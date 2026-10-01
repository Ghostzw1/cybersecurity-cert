# Course 2 — Play It Safe: Manage Security Risks

**Coverage:** covered according to reported study progress. **Document type:** newly prepared AI-assisted revision summary; no audit or lab result is claimed here.

## 1. Describe risk before choosing a control

A useful risk statement connects an asset, a weakness, a plausible event, and its effect. For example: “A shared administrator account makes it difficult to attribute changes to the order database, increasing the risk that an unauthorized change goes unnoticed.” This is an original fictional scenario.

Risk assessment considers context, existing safeguards, likelihood, and impact. A severe weakness on an isolated test device may have a different priority from the same weakness on a public service holding customer records.

Common responses include reducing a risk, avoiding the activity, transferring part of the financial impact, or accepting a documented residual risk. The responsible business owner makes that decision; a security analyst supplies evidence and advice.

## 2. Frameworks and controls

A framework helps organize work and communicate objectives. A control is a specific safeguard. Examples include multi-factor authentication, access reviews, staff training, logging, backups, and physical access restrictions. Controls can prevent, detect, or help correct problems; several controls often work together.

NIST CSF **2.0** organizes outcomes under **Govern, Identify, Protect, Detect, Respond, and Recover**. Older learning materials may describe the five functions in CSF 1.1; Govern was added in 2.0. These functions describe connected areas of work, not a rigid sequence of incident-response steps. [NIST reference](https://www.nist.gov/news-events/news/2024/02/nist-releases-version-20-landmark-cybersecurity-framework)

The NIST Risk Management Framework provides another structure: prepare, categorize, select, implement, assess, authorize, and monitor. It emphasizes choosing controls in context and checking their operation over time. [NIST RMF](https://csrc.nist.gov/projects/risk-management/about-rmf)

Secure design principles include granting only necessary access, using multiple protective layers, checking access at the point of use, and selecting defaults that do not unnecessarily expose a resource. A secure default still needs testing against the actual business workflow.

## 3. Security audits

An audit compares evidence against a defined set of criteria. Start with the scope: which systems, information, period, and requirements are being assessed? Then record evidence, findings, impact, recommendations, and responsible owners.

**Original example — not a completed audit:** If a policy requires periodic account reviews, the review procedure alone does not prove reviews occurred. A dated review record and evidence that identified access was corrected would be stronger support.

Avoid inventing a pass or fail when evidence is missing. State the gap and the next evidence needed. Distinguish a control that exists on paper from one that operates effectively.

## 4. Logs and SIEM

A log records an event from a particular source. A SIEM can aggregate logs, support searches, and generate alerts from rules or other detection logic. The quality of an investigation depends on the underlying data and its coverage.

For a suspicious sign-in, useful questions include:

- Which account, device, time zone, source address, and application are involved?
- Was the attempt successful, and did later activity occur?
- Could a known administrative task, user mistake, or logging issue explain it?
- Which other source can confirm or challenge the hypothesis?

A dashboard summarizes selected data. It does not guarantee that unmonitored systems are safe. False positives and missed detections both matter when evaluating a rule.

## 5. Playbooks and incident response

A playbook describes how to handle a defined situation: trigger, checks, responsible people, escalation, actions, communication, and closure criteria. A runbook can provide more detailed operational steps. Automation can support those steps, but a disruptive action should follow the organization's authorization rules.

Response work includes preparing, detecting and analyzing, containing the problem, removing its cause, recovering service, and learning from the incident. Record what was done and why. A service being online again is not enough; verify that the cause and persistence mechanisms have been addressed and normal operation restored.

**Revision prompt:** Draft the questions an analyst should ask about repeated failed sign-ins. Separate observations from possible causes and explain what would justify escalation. Do not assume every failure is an intrusion.

**Course reference:** [Play It Safe: Manage Security Risks](https://www.coursera.org/learn/manage-security-risks). See the [practical work register](../LABS.md) for the audit activity and evidence status.
