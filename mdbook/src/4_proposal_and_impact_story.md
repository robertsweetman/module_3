# Proposal and Impact Story <!-- 300 words -->

To help communicate the changes to a non technical audience we can focus on the overall categories of risk we're addressing. Using the NCSC framework allows us to say that all the requirements of the Cyber Assessment Framework (CAF) are now at the **Achieved** level. Going into slightly more detail:

* Database access is only available to internal staff
* Ongoing logging & monitoring will alert us to any application issues
* Ongoing Security scanning will highlight any AWS config and resource issues
* Moving the `ai_summary` Lambda API calls to AWS Bedrock increases security

Now the only external interaction the AWS hosted environment has is to send the "respond to this tender" message and this is only ever an outbound email. This, combined with ongoing logging & scanning results in a very secure application

## Implementation Costs



## Quantifying Impact

Failure to act, especially in the case of PostgreSQL access, could result in the takeover of the database. This is a particularly unpleasant outcome which an attacker could significantly missuse by storing their own illegal information on there, simply deleting or stealing the original content for ransom.

While this particular application is based entirely on publically available data the reputational damage for any sort of breach, especially for a consultancy service, is likely to be significant.

Global Cyberattacks are only increasing in frequency (CheckPoint, 2024) REF: https://blog.checkpoint.com/research/check-point-research-reports-highest-increase-of-global-cyber-attacks-seen-in-last-two-years-a-30-increase-in-q2-2024-global-cyber-attacks/ with reputation being something that would be impacted (CYE Insights, 2024) REF: https://cyesec.com/blog/hidden-costs-cyberattack-impact-reputation 

It only takes one decision maker backing off awarding a single contract to make a £5-100 million dent in a companies revenue. Reputation has a huge impact on the contract awards process and likelyhood of a positive outcome.



<!-- 
WHAT ARE THE RISKS IF YOU DON'T DO IT vs. IF YOU DO
IMPORTANT: Put an actual money value on this
IMPORTANT: look at feedback on Module 2 for this as well
-->

<!-- 
* Develop an impact story that illustrates the ROI of propose security enhancements. Highlight potential cost savings, revenue improvements and the enablement of other critical organizational functions.

* GUIDANCE USE: Reference the Business Impact Story Guide to structure the narrative effectivey, ensuring the benefits are clear and compelling.

-->

<!-- MARKING RUBRIC

PROPOSE A SOLUTION TO INCREASE THE SECURITY OF THE NETWORK/DATA
* Develop a sophisticated solution to address the identified vulnerabilities and risks
* Thoroughly explain how the proposed solution aligns with industry standards/regulations
  * Explain in a clear and concise manner
  * Include additional insights and examples

Evidence this in Secton 3 also!

-->