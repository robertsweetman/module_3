# Evaluation of Current State <!-- 1000 words -->

## Endpoint Inventory

Since our application is cloud-based, primarily using serverless functions, we have some unique considerations that aren't 

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