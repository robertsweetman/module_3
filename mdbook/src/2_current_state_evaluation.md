# Evaluation of Current State <!-- 1000 words -->

Evaluating security for a function based serverless application is different than a traditional hub/spoke or point-to-point network because the essential platform is entirely different. As can be seen from the figure below, a serverless architecture means developers focus on the application while everything else is abstracted away or become the responsibility of the cloud platform provider.

![Serverless Shared Responsibility](./images/Serverless_Shared_Responsibility.png)
Figure 1 : Serverless Responsibility (Cloud Security Alliance 2023:11)

Now, there is still _shared_ responsibility because although many vulnerabilities have been removed there are new issues that arise that are unique to a serverless approach.

![Setup and Deployment Stage Threats](./images/Setup_Deployment_Stage_Threats.png)
Figure 2 : Setup and Deployment Stage Threats (Cloud Security Alliance 2023:20)

For example, if we happen to commit secrets to code that would be an extreme "deployment stage" threat that could expose our application to being taken over. You certainly couldn't expect the cloud provider to take responsibility for this mistake.

Serverless applications do have additional advantages over other approaches, primarily cost. 

They are only charged on a "per-execution" basis so having a data-pipeline run each day and possibly instansiate a dozen functions and destroy them after a few minutes means the running cost of this application is less than $1 per day.

## Endpoint Inventory

![Initial Application Diagram](./images/initial-state-final.drawio.png)
Figure 3: Initial Application Diagram

Our application is entirely cloud based and consists primarily of AWS Lambda (serverless) functions, an event-driven chain and PostgreSQL as a data store plus state record.  

### AWS RDS (PostgreSQL) db connection
The first serverless function `postgres_dataload` goes and gets the latest electronic tenders. Anything this function retrieves is stored in the RDS PostgreSQL database. 

The database is updated by subsequent lambda functions as the tender information passes through the ML/AI pipeline. The database stores a record of what has happened at each Lambda step and is used for debugging issues with the data pipeline. In future it could also be used as a source for further ML improvements via re-inforcement learning or to expand the amount of training data on which to retrain the model

Open to the internet for ease of development from Windows machine using PgAdmin 4 application. REF: 
TODO: 
 - Add link to docs
 - Find out how encryption works to/from here

TODO: Look at the CVE site for the things in the system

### GitHub action pipelines
Pipelines deploy Terraform defined resources into AWS and also to build the AWS Lambdas (in Rust) and upload them to AWS S3. These pipelines use GitHub action secrets so no password or other sensitive values are ever committed to the GitHub repo for attackers to re-use.
<!-- TODO: maybe cut this down rather -->
Every interaction with the AWS resources is run via GitHub action pipelines all the secrets needed to access the environment are stored as GitHub Action Secrets, which are all secured via 2-Factor-Authentication (2FA) linked to the developers GitHub account.

### AWS S3
To allow multiple developers to work on the project there is an S3 object location for the Terraform state file. This use of an S3 bucket to hold the Terraform state file is defined in the code.

Having the state file in S3 allows for multiple developers to make changes to a common state file, rather than maintaining their own local state file copy. 

The S3 bucket is also where the AWS Lambdas are uploaded to when built. Each Lambda function grabs the .zip file from it's bucket location and runs it as part of it's execution process.

### AWS Lambda functions & queues
All the Lambda functions exist within the AWS environment. AWS Simple Queue Service is used to trigger and initialize new function instances when a message they're interested in lands on the queue and each Lambda post results onto the next queue in the chain.

<!-- 
#### Postgres-dataload
This is the function that kicks off the whole process of deciding which tenders to actually bid on. It's triggered on a schedule so at 09:00 it goes and get's the tender info and puts what's there on an SQS queue as well as updating the Post

#### pdf processor
If there's a tender containing a pdf it'll pick that tenders pdf url off the SQS queue, read the text from the PDF and update the database with the PDF content. This allows the PDF content to be supplied to the ML layer or later to the AI lambda for further analysis. 

#### ml processor
Tenders without PDF content go straight onto the ai_summary queue becase the ML setup hasn't got enough context to accurately predict wheter to bid on something or not. If there is a PDF then the ML processor will return a score  

#### ai summary
Takes items off the ai_summary queue and sends their content to a Claude Endpoint using an acount Key that's been generated by a developer and added to the project's GitHub secrets account

#### sns
-->

### Anthropic Claude API endpoint
The AI Summary Lambda makes a call over the web to Claude's API endpoint via https. It is secured via an API Key that has been stored in the GitHub action secrets that is passed in to the AWS Lambda environment at the point the pipeline runs to build the AI Summary lambda so this can be considered secure. 

### AWS Simple Notification Service
To alert the sales team to a potential bid this service sends an email to a recipient list. In the development phase all emails have to be validated by the recipient agreeing to receive emails from this particular source. For security, the SNS service uses a real domain account which has also been independently validated/approved by the domain owner via DNS settings.

### AWS IAM IMPORTANT: DEFINITELY COVER THIS

https://genai.owasp.org/llm-top-10/ <-- use as a reference for analysis


- ENDPOINT LIST
 - ROLE
 - RISK/SIGNIFICANCE


IMPORTANT: DO NOT TALK ABOUT REMEDIATION AT ALL IN THIS SECTION
 - JUST THE DIAGRAM AND ENDPOINT INVENTORY HERE
 - IN no particular order

<!-- 
 * draw IO for network diagram
 * look at OWASP AI/LLM stuff
 * explain topology i.e. ALL CLOUD or STAR or something else
 * what are the key concepts on the diagram
 * argue for why improvements made, justify decisions
 * diagram for after, for example
 * support the WHY with industry best practice
  * GDPR is that's relevant
  * CVE's severity etc.

MILESTONE 3 - score the likelyhood of a breach vs. a framework. 
-->

<!--
* Create an Inventory of accessible network endpointscategorized by role, operating system and significance, using advanced scanning tools

* Create a basic network diagram that can include components like routers, switches, servers and workstations
-->

## Cybersecurity Analysis

Based on the **NCSC Cyber Assessment Framework (CAF)** and **ISO 27001:2022**, this analysis evaluates each endpoint against UK cybersecurity best practices. 

The NCSC CAF provides outcome-driven principles specifically designed for UK organisations, while ISO 27001 defines internationally recognised information security management standards.  

For AI/ML we can use the **OWASP LLM Top 10** and **ENISA's AI Cybersecurity Guidelines** which cover risks in AI systems and data processing.

### Risk Assessment Matrix

The following table applies **ISO 27005** risk management methodology for systematic risk identification, analysis, and evaluation, while using **NCSC CAF outcome assessments** to evaluate current security posture. 

**NCSC CAF outcomes** are rated as:
- **Not Achieved**: Significant security gaps, immediate attention required
- **Partially Achieved**: Some controls in place but with issues that need addressing
- **Achieved**: Security effectively implemented and maintained

Using these outcomes helps non-technical sponsors understand the current state of the system with respect to security.

| Endpoint | Role | Primary Risks | NCSC CAF Assessment | Impact if Breached |
|----------|------|---------------|-------------------|-------------------|
| **AWS RDS (PostgreSQL)** | Data storage and state management | • Unauthorized data access<br/>• Data manipulation/corruption<br/>• Credential exposure<br/>• Public internet exposure | **Not Achieved** | Complete tender data compromise, competitive intelligence loss |
| **GitHub Action Pipelines** | CI/CD deployment and secrets management | • Secret exposure in logs<br/>• Pipeline injection attacks<br/>• Unauthorized deployments<br/> | **Partially Achieved** | Full AWS environment takeover, code tampering, infrastructure manipulation, backdoor deployment |
| **AWS S3 Bucket** | Terraform state and Lambda code storage | • Terraform state exposure<br/>• Lambda code tampering<br/>• Unauthorized object access<br/>• Bucket policy misconfiguration | **Achieved** | Infrastructure secrets exposure, code intellectual property theft, deployment manipulation |
| **AWS Lambda Functions** | Core business logic processing | • Function injection attacks<br/>• Environment variable exposure<br/>• Excessive permissions<br/>• Dependency vulnerabilities | **Partially Achieved** | Business logic bypass, data processing manipulation, service disruption |
| **AWS SQS Queues** | Inter-service communication | • Message tampering<br/>• Queue flooding (DoS)<br/>• Dead letter queue exposure<br/>• Cross-service privilege escalation | **Achieved** | Data pipeline disruption, message manipulation, service degradation |
| **Anthropic Claude API** | AI/ML text analysis and summarization | • Prompt injection attacks<br/>• API key compromise<br/>• Model poisoning via crafted inputs | **Achieved** | Tender data exposure to third party, AI system manipulation |
| **AWS SNS** | Notification and alerting system | • Email spoofing/phishing<br/>• Unauthorized subscription access<br/>• Message interception<br/>• Service abuse for spam | **Achieved** | False notifications, information disclosure via email, social engineering attacks |
| **AWS IAM** | Identity and access management | • Privilege escalation<br/>• Role assumption abuse<br/>• Policy misconfigurations<br/>• Credential exposure | **Achieved** | Complete AWS account takeover, cross-service access, data exfiltration, resource manipulation |

Where endpoints are assessed as **Achieved** this is primarily through the use of 2 Factor Authentication both to access AWS and GitHub, especially when it comes to using or storing credentials or secrets. 

We can also use AWS internal tools to help identify or further qualify risks. AWS has their own security review tooling which looks at the underlying infrastructure for issues. 

![AWS Security Review](./images/aws_security_review.png)
Figure 4: AWS Security Review - _clearly highlights PostgreSQL open port risk_

At the database level, while there are vulnerabilities they are at such a low possibility of being exploited that it's not worth worrying about.

![PostrgeSQL Vulnerabilities](./images/Postgres_Vulnerabilities.png)
Figure 5: PostgreSQL vulnerabilities

Very low EPSS scores indicate that these exploits are unlikely to be effectively executed in the wild (REF: https://www.first.org/epss/) 

Very often it's security **misconfiguration** that leads to vulnerabilities (REF: https://www.huntress.com/cybersecurity-101/topics/what-is-security-misconfiguration) which is where automated tools like AWS Security Review comes in to play, pointing out common issues that might easily lead to data compromise.

Assessing the CI/CD/GitHub pipeline as **Partially Achieved** is actually a bit harsh. From a developer access, secrets management and deployment pipeline execution point of view the use of 2FA means that this is all very secure.

Unfortunately it's not all about secrets here. 

There might be issues within the resources deployed by Terraform, again sitting within their configuration, as well as the actual Rust code or the crates (libraries) the Lambdas are built from. We will get into mitigation steps for these issues in the next section though.

We can also make some architectural choices to mitigate issues further and also address "platform risk" (REF: https://www.startupillustrated.com/Archive/Platform-Risk/) which is the over-reliance on a particular platform or service in order for the application to function.


TODO: 
- AWS IAM
 - BEST PRACTICES ARE WHAT?
- TOOLS ADVANTAGES AND DISADVANTAGES
- THREAT ANALYSIS 
 - ESPECIALLY IN RELATION TO DATA
 - WHAT SCANNING TOOLS APPLY HERE?

* "well architected framework"
* AWS security advisor <- I've got a picture for this now
* Trivy security analysis for Terraform
* Other 'best practice' frameworks for cloud/serverless
* WHAT SECURITY FRAMEWORKS APPLY TO THE AI COMPONENT

https://www.cvedetails.com/vendor/336/ <- postgreSQL

https://medium.com/@simardeep.oberoi/unveiling-github-actions-vulnerabilities-a-comprehensive-technical-guide-to-attack-vectors-and-6a26a83e9fb2

https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator

IMPORTANT: DO NOT TALK ABOUT REMEDIATION AT ALL IN THIS SECTION

### AWS RDS (PostgreSQL) db connection
As can be seen from the AWS RDS security group config, the AWS RDS db connection is open to the internet. It was set up this way initially so that the application developers could quickly validate and iterate on the database design from their local machines.

TODO: Add code pic here

While there is definitely a convenience to be had from quickly running queries locally as the solution is being developed, access over the web secured by a simple username/password puts this as a high risk activity. 

TODO: Is there an AWS based web interface from which you can run queries instead??

Open to the internet for ease of development from Windows machine using PgAdmin 4 application. REF: https://www.pgadmin.org/
TODO: 
 - Add link to docs
 - Find out how encryption works to/from here
 - Run wireshark on connections to the db via Pgadmin to see whether or not these are encrypted

### GitHub Action Pipelines


### AWS S3
Upload to S3 is only available via the GitHub action pipelines and all the secrets needed to access the environment are stored as GitHub Action Secrets, which are all secured via 2-Factor-Authentication (2FA) 




<!-- 
- clear text/issues
-->

<!-- 
* Provide an overview of existing accessible and relevant protection mechanisms such as anti-virus, anti-malware and EDR systems, encryption and access controls

* Analyse the efficiency of these tools, highlight their advantages and disadvantages

* Analyse the effectiveness of protections and IDS/IPS systmes such as firewalls, VPNs, and endpoint protection software.

* Identify areas needing improvement, focusing on deficiencies that could expose endpoints to threats.

* My project is endpoint and data protection, out of the examples

-->

<!-- MARKING RUBRIC

CONDUCTS COMPREHENSIVE RESEARCH
* clear and detailed explanation of the network design, management and security
* include insightful examples and best practices
* create a detailed and well organised network diagram which...
  * accurately represents the network endpoints and their roles

EVALUATE A DIGITAL OR DATA NETWORK FOR COMMON VULNERABILITIES AND RISKS
* Conduct a thorough vulnerability assessment using industry standard tools
* analyze findings and identifies common vulnerabilities and risks in...
  * a clear and concise manner with...
  * additional insights and examples 

All this needs to be evidenced in this section

-->