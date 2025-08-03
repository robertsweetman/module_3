# Overview <!-- 500 words -->

## Cybersecurity Significance

Since we're all firmly rooted in the digital age there's no aspect of our lives that don't rely on robust cybersecurity. 

As with many technical domains it's very easy to stress the hardware/tools and buzzwords but we have to remain focussed on the goal - protecting valuable information about ourselves, our employer or our clients. 

With this in mind we can take steps to ensure we're a harder target. You don't have to out-run the bear, you just need to be faster than your peers but there are still minimum standards to maintain. Hope is not a viable strategy.

Any emerging technology hasn't been as "battle tested", best practices take time to become established. This example about accessing AWS S3 buckets REF: (1) from 2018: 

```text
For 24652 scanned buckets I was able to collect files from 5241 buckets (21%) and to upload arbitrary files to 1365 buckets (6%). 
```

Of course things will  have improved since then, but they're still not great according to Tenable REF:

```text
The number of organizations with triple-threat cloud instances — “publicly exposed, critically vulnerable and highly privileged” — declined from 38% between January and June 2024 to 29% between October 2024 and March 2025.
```

Similarly unguarded access to Internet of Things (IoT) devices has allowed hackers to control huge "botnets", computers acting together to (usually) launch Denial Of Service attacks at targets. 

In addition these are often state-sponsored and designed to take their oppositions sites and services off-line at critical periods. REF: China botnet 

The three hundred pound gorilla in the room (to borrow a US phrase) is AI, lending everyone a potential foot-gun. 

Spending on AI (capital investment) has balloned and it's contribution to US GDP so far this year has exceeded US consumer spending. REF: 

Cybersecurity as it relates to AI is a new field with so many sharp edges that it's already challenging to keep up with. Here are some (very scary) recent headlines: 

* REF: Exfiltraging passwords from Chrome password manager 
    https://www.forbes.com/sites/daveywinder/2025/03/21/google-chrome-passwords-alert-beware-the-rise-of-the-ai-infostealers/

* REF: Enthusiastic vibe coders committing API keys to repos
    https://www.aikido.dev/blog/vibe-check-the-vibe-coders-security-checklist

* REF: Enabling a huge increase in ransomware and highly targeted attacks https://www.forbes.com/sites/daveywinder/2025/03/25/massive-surge-in-ransomware-attacks-ai-and-2fa-bypass-to-blame/

Even leaking private chats into google search results REF: https://arstechnica.com/tech-policy/2025/08/chatgpt-users-shocked-to-learn-their-chats-were-in-google-search-results/

So while it's clear that AI can contribute to profitability and deliver value it's certainly not all roses.
<!--
Emphasize the strategic importance of cybersecurity in addressing the business implications of emerging technologies like cloud computing, IoT and AI. 

Highlight how these technologies, while enhancing capabilities, also introduce new vulnerabilities
-->

## Role and Project Impact

The eTenders project (from module 2) has allowed me to really expand my programming skills around AWS, automation, serverless functions and AI/ML.

Since the entire project is automatically built in Amazon's cloud (AWS) this sits on top of a number of secret keys that mustn't be exposed.

These secrets are necessary for the automation to work but mustn't be accessible as they would allow someone to create their own infrastructure for free in the AWS account. 

If, for example the Claude API key wasn't in a GitHub secret but had been (mistakenly) included in a commit then someone would be able to use this to pose their own questions to Claude for free.

Exposure of some secrets would also potentially allow a bad actor to compromise the project's AWS RDS PostgreSQL database or delete things from it even.

<!--
Outline your responsibilities in managing network security and describe this project's alignment with your professional growth. 

Stress the importance of enhancing security to prevent cyber threats and maintain organizational integrity.
-->
