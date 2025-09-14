# Overview

## Cybersecurity Significance

Nowadays there's no aspect of our lives that don't rely on robust cybersecurity to protect valuable information about ourselves, our employer or our clients. 

Unfortunately new technology doesn't arrive fully "battle tested" and best practices take time to become established. Results below from scanning AWS S3 buckets from 7 years ago (Rzepa, 2018): 

```text
For 24652 scanned buckets I was able to collect files from 5241 buckets (21%) and to upload arbitrary files to 1365 buckets (6%). 
```

Of course things will have improved but they're still not great according to Tenable (2025)

```text
The number of organizations with triple-threat cloud instances — “publicly exposed, critically vulnerable and highly privileged” — declined from 38% between January and June 2024 to 29% between October 2024 and March 2025.
```

Similarly unguarded access to Internet of Things (IoT) devices has allowed hackers to control huge "botnets", computers acting together to launch Denial Of Service attacks at targets. 

These botnets are often state-sponsored and designed to take opposition sites and services off-line at critical periods (Godwin, 2024).

While spending on AI (capital investment) has balloned and it's contribution to US GDP so far this year has exceeded US consumer spending. (Kawa, 2025)

Cybersecurity as it relates to AI is a new field that is already challenging to keep up with. Here are some recent incidents that will no doubt keep Chief Information Security Officers awake: 

* AI exfiltrating passwords from Chrome password manager (Winder, 2025)

* Enthusiastic vibe coders committing API keys to repos (Jackson, 2025)

* AI enabling a huge increase in ransomware (Winder, 2025)

* Private AI chats leaking into google search results (Arstechnica.com, 2025) 

Finally, the overall picture from the Cloud Security Alliance (cloudsecurityalliance.org, 2025:13) provides a particularly uncomfortable statistic.

```text
More than a third of organizations with AI workloads (34%) have already experienced an AI-related breach, raising urgent questions about AI security readiness and risk management
```

So while it's clear that AI can contribute to profitability and deliver value it's certainly not all roses.

## Role and Project Impact

The eTenders project (robertsweetman, 2025) has allowed me to really expand my programming skills around AWS, automation, serverless functions and AI/ML. 

The project is automatically built in Amazon's cloud (AWS) and relies on a number of secret keys. As the sole developer of this application it's been my responsibility to make sure any secrets or sensitive information doesn't immediately leak because this would allow someone to create their own infrastructure for free in the root AWS account. 

If, for example the Claude API key wasn't in a GitHub secret but had been (mistakenly) included in a commit then someone would be able to use this to pose their own questions to Claude for free. Exposure of some secrets would also potentially allow a bad actor to compromise the project's AWS RDS PostgreSQL database or delete things from it even. 

The initial architecture, while developer friendly, now needs changing to enforce security best practice.
