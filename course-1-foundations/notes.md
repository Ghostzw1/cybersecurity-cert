# Course 1 — Foundations of Cybersecurity

**Coverage:** covered according to reported study progress. **Document type:** AI-assisted revision summary prepared on 30 September 2026, not a notebook transcription or lab submission.

## 1. Security work and business purpose

Cybersecurity protects systems, services, and information against harm. The business reason is practical: people need dependable services, accurate records, and appropriate privacy.

An entry-level analyst may review alerts, collect relevant context, document findings, follow procedures, and escalate issues. Clear writing matters because the next person must understand what happened and which evidence supports a decision. An alert is a reason to investigate; it is not, by itself, proof of an attack.

Useful habits include asking precise questions, checking assumptions, protecting sensitive information, and recording uncertainty. Technical vocabulary helps communication, but an explanation should still make sense to someone outside the security team.

## 2. Threats, weaknesses, and impact

| Term | Working meaning | Original example |
|---|---|---|
| Asset | Something worth protecting | A shop's customer-order database |
| Threat | A potential cause of harm | Someone attempting unauthorized access |
| Vulnerability | A weakness that could be exploited | An account retaining access after its owner leaves |
| Risk | Potential loss considered in context of likelihood and impact | Exposure of customer records through that account |
| Control | A safeguard that changes risk | Account offboarding and access reviews |

Common attack concepts include phishing, malicious software, social engineering, password attacks, and attacks on application inputs. Different attacker motives lead to different targets: money, disruption, espionage, or a personal grievance. Historical incidents help explain why modern controls exist; recognizing a famous incident does not replace investigating today's evidence.

## 3. Security domains and the CIA triad

The course introduces eight broad domains: security and risk management; asset security; security architecture and engineering; communication and network security; identity and access management; security assessment and testing; security operations; and software development security. These categories show how different responsibilities fit together. Studying them here does not imply a CISSP credential.

The **CIA triad** is a useful way to describe a protection goal:

- **Confidentiality:** only appropriate people or systems can access information.
- **Integrity:** information and system state remain accurate and are changed appropriately.
- **Availability:** authorized users can access needed resources when required.

For an order system, confidentiality protects customer details, integrity protects quantities and payment records, and availability lets staff serve customers. A single incident can affect more than one goal.

Frameworks organize security work. Policies state expectations. Controls help put those expectations into practice. Compliance concerns applicable requirements; it is not a guarantee that every risk has been addressed.

## 4. Ethics, tools, and communication

Security work requires permission and appropriate handling of information. Access should be limited to the task, and findings should be reported through the agreed channel. An analyst should distinguish a confirmed observation, a possible explanation, and a recommended next step.

| Tool or language | Introductory purpose |
|---|---|
| SIEM | Collect and search security event data; support alerting and investigation |
| Network protocol analyzer | Inspect captured network traffic |
| Linux shell | Interact with an operating system through commands |
| SQL | Query structured data in relational databases |
| Python | Express repeatable logic for tasks such as processing data |

These are introductory roles, not a claim of proficiency in every tool. Later notes develop Linux and SQL in more detail.

## Explain it back

For the fictional order system above, identify one asset, one threat, one weakness, and one suitable control. Then describe what evidence would show whether the control works. This is a revision prompt, not a completed assessment.

**Course reference:** [Foundations of Cybersecurity](https://www.coursera.org/learn/foundations-of-cybersecurity). See [sources and authorship](../SOURCES.md) and the [practical work register](../LABS.md).
