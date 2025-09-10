# Overview <!-- 500 words -->

## Cybersecurity Significance

Since we're all firmly rooted in the digital age there's no aspect of our lives that don't rely on robust cybersecurity. 

As with aany technical domain it's very easy to stress the hardware, tools and buzzwords but loose sight of the goal - protecting valuable information about ourselves, our employer or our clients. 

Emerging technology doesn't arrive fully "battle tested" and best practices take time to become established. This shows security around AWS S3 buckets from 7 years ago (Rzepa, 2018): 

```text
For 24652 scanned buckets I was able to collect files from 5241 buckets (21%) and to upload arbitrary files to 1365 buckets (6%). 
```

Of course things will have improved since then, but they're still not great according to Tenable (2025)

```text
The number of organizations with triple-threat cloud instances — “publicly exposed, critically vulnerable and highly privileged” — declined from 38% between January and June 2024 to 29% between October 2024 and March 2025.
```

Still surprisingly high really.

Similarly unguarded access to Internet of Things (IoT) devices has allowed hackers to control huge "botnets", computers acting together to (usually) launch Denial Of Service attacks at targets. 

These botnets are often state-sponsored and designed to take opposition sites and services off-line at critical periods (Godwin, 2024).

Now the three hundred pound gorilla in the room is AI, lending everyone a potential foot-gun. 

Spending on AI (capital investment) has balloned and it's contribution to US GDP so far this year has exceeded US consumer spending. (Kawa, 2025)

Cybersecurity as it relates to AI is a new field with so many sharp edges that it's already challenging to keep up with. Here are some (very scary) recent incidents: 

* Exfiltraging passwords from Chrome password manager (Winder, 2025)

* Enthusiastic vibe coders committing API keys to repos (Jackson, 2025)

* Enabling a huge increase in ransomware and highly targeted attacks (Winder, 2025)

Even leaking private chats into google search results (Arstechnica.com, 2025)

So while it's clear that AI can contribute to profitability and deliver value it's certainly not all roses.
<!--
Emphasize the strategic importance of cybersecurity in addressing the business implications of emerging technologies like cloud computing, IoT and AI. 

Highlight how these technologies, while enhancing capabilities, also introduce new vulnerabilities
-->

## Role and Project Impact

The eTenders project (from module 2) has allowed me to really expand my programming skills around AWS, automation, serverless functions and AI/ML.

Since the entire project is automatically built in Amazon's cloud (AWS) this sits on top of a number of secret keys.

These secrets are necessary for the automation to work but mustn't be accessible as they would allow someone to create their own infrastructure for free in the AWS account. 

If, for example the Claude API key wasn't in a GitHub secret but had been (mistakenly) included in a commit then someone would be able to use this to pose their own questions to Claude for free.

Exposure of some secrets would also potentially allow a bad actor to compromise the project's AWS RDS PostgreSQL database or delete things from it even.

Happily, due to 2 Factor Authentication (Microsoft, n.d.) , all project secrets are protected but still available (via GitHub actions) to drive all the deployment and lambda build automation.

<!--
Outline your responsibilities in managing network security and describe this project's alignment with your professional growth. 

Stress the importance of enhancing security to prevent cyber threats and maintain organizational integrity.
-->
