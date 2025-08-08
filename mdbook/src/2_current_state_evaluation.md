# Evaluation of Current State <!-- 1000 words -->

## Endpoint Inventory

TODO: Insert current state diagram here

Our application is entirely cloud based (on AWS) and consists primarily of AWS Lambda (serverless) functions and AWS RDS using PostgreSQL. 

There 'are' a number of endpoints however as well as a function that sends emails to registered addresses. We still have to prevent things like unauthorised access to S3 buckets, the PostgreSQL db and un-authorised AWS Lambda executions.

### AWS RDS (PostgreSQL) db connection


### AWS S3
Used as an upload target for AWS Lambda's built via GitHub pipelines as well as the host for the Terraform state file. 

Having the state file in S3 allows for multiple developers to make changes to a common state file, rather than maintaining their own local state file copy. 


### AWS Lambda functions

#### Postgres-dataload

#### pdf processor

#### ml processor

#### ai summary

#### sns

### AWS IAM

https://genai.owasp.org/llm-top-10/ <-- use as a reference for analysis


TODO: 
- NETWORK DIAGRAM (current state)
  - Are there any automation tools that will WORK and produce a diagram from terraform automatically??
  - https://github.com/patrickchugh/terravision
  - pluralith
  - terraform graph - run command - hand it to something else? Graphviz?
  - terraform visual, can run in CICD

- ENDPOINT LIST
 - ROLE
 - RISK/SIGNIFICANCE


IMPORTANT: DO NOT TALK ABOUT REMEDIATION AT ALL IN THIS SECTION
 - JUST THE DIAGRAM AND ENDPOINT INVENTORY HERE
 - IN no particular order

### AWS RDS (PostgreSQL) db connection
Open to the internet for ease of development from Windows machine using PgAdmin 4 application. REF: 
TODO: 
 - Add link to docs
 - Find out how encryption works to/from here

TODO: Look at the CVE site for the things in the system

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

IMPORTANT: What Frameworks of references are we going to use for our CyberSecurity analysis?

Since our application is cloud-based and primarily uses serverless functions we have some things to consider that don't fall in the usual legacy hardware/virtual machine/networking approach.

TODO: 
- AWS IAM
 - BEST PRACTICES ARE WHAT?
- TOOLS ADVANTAGES AND DISADVANTAGES
- THREAT ANALYSIS 
 - ESPECIALLY IN RELATION TO DATA
 - WHAT SCANNING TOOLS APPLY HERE?

* "well architected framework"
* AWS security advisor
* Trivy security analysis for Terraform
* Other 'best practice' frameworks for cloud/serverless
* WHAT SECURITY FRAMEWORKS APPLY TO THE AI COMPONENT

IMPORTANT: DO NOT TALK ABOUT REMEDIATION AT ALL IN THIS SECTION

### AWS RDS (PostgreSQL) db connection
Open to the internet, only protected via username/password from local PC which is clearly bad. High risk of exposure vs. convenience of being able to run queries locally.

Open to the internet for ease of development from Windows machine using PgAdmin 4 application. REF: https://www.pgadmin.org/
TODO: 
 - Add link to docs
 - Find out how encryption works to/from here

### AWS S3
#### AWS Lamda zip files
#### Terraform State file

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