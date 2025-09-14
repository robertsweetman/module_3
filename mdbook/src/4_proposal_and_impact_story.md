# Proposal and Impact Story

To help communicate the changes to a non technical audience we can use the NCSC framework and say allows us to say  our proposed changes reach **Achieved** level across all requirements: 

* **Database access** - Internal staff only via bastion server
* **Monitoring** - Real time alerts for application issues
* **Security scanning** - AWS config and resource issues
* **API security** - Migrate to AWS Bedrock from external API

Now the only external interaction the AWS hosted environment has is to send the "respond to this tender" message and this is only ever an outbound email. This, combined with ongoing logging & scanning results in a very secure application

## Implementation Costs

| Item | Monthly Cost | Notes |
|------|------|-------|
| Base cost | £20 | Historical 3 month average |
| EC2 bastion server | +£15 | ($0.025 per hour x 744 hours) @ 0.75 pounds per USD (AWS, 2025) |
| Move to AWS Bedrock | £0 | Cost neutral vs. current API |
| Enhance Logging/Monitoring | +£10 | Increases data flow |
| Developer Time | estimate 1 -5 hourse | one off cost |

Even doubling the running cost of the app by adding a bastion server isn't nearly as damaging as suffering reputational damage.

## Risk vs Investment

Failure to act, especially in the case of a consultancy, means any reputational damage is likely to be significant.

Global Cyberattacks are only increasing in frequency (CheckPoint, 2024) with reputation being something that would be impacted (CYE Insights, 2024)

It only takes one decision maker hesitating on a contract award to make a £5-100 million dent in a companies revenue because reputation has a huge impact on the contract awards process and likelyhood of a positive outcome.
