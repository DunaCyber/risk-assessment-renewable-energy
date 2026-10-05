# Cybersecurity Risk Assessment: SolaraVive Helios Platform

> **Note:** This is a simulated risk assessment based on a fictional company. All organizational details, assumptions, and scores are illustrative and were created for learning purposes.

## Executive Summary

SolaraVive is a renewable energy company headquartered in Washington, DC, operating solar and wind projects across the United States. Its **Helios platform** is a cloud-based system (hosted on AWS) that monitors energy production, system health, and operational performance, and supports regulatory reporting.

This assessment identifies nine priority risks to Helios, scores them using a 5x5 likelihood-and-impact method, maps each control to **NIST CSF 2.0** and **ISO/IEC 27001:2022 Annex A**, and recommends where to act first.

**Top three priorities:**

1. **Stolen or phished credentials** (R1, R4): the most likely path to Helios. Enforce phishing-resistant MFA and email authentication first.
2. **Ransomware on cloud workloads** (R2): the highest-impact event. Immutable backups and tested restores shrink the damage the most.
3. **Third-party and API compromise** (R3): Helios depends on outside connections, so vendor review and API limits should follow quickly.

---

## 1. Scope, Method, and Assumptions

**In scope:** The Helios platform (dashboards, APIs, databases), employee accounts with Helios access, SolaraVive's AWS environment, and third-party integrations.

**Out of scope:** Physical security at generation sites, detailed operational technology (OT) design, and financial systems.

**Method:** Qualitative assessment guided by NIST CSF 2.0. Each risk is scored on likelihood and impact (1 to 5), multiplied to give a score, and re-scored after planned controls to show residual risk.

| Score | Rating |
|-------|--------|
| 1-4 | Low |
| 5-9 | Medium |
| 10-16 | High |
| 20-25 | Critical |

**Assumptions (simulated):**

- Helios is the system of record for production data used in compliance reporting.
- Helios data flows from site systems into AWS. The exact OT connection is not modeled, so any OT-related risk is flagged as an assumption.
- Staff authenticate with passwords today, with MFA not yet enforced everywhere.
- Regulatory obligations (for example, whether NERC CIP applies at SolaraVive's size) would be confirmed with legal and compliance in a real engagement.

---

## 2. Crown Jewel and Key Assets

**Crown jewel: Helios Operations Platform.** It holds operational energy data, supports decision-making, is required for compliance reporting, and carries a high-risk classification.

| Asset | Description |
|-------|-------------|
| Helios platform | Main monitoring system for energy production |
| Operational databases | Store energy output and system data |
| Employee accounts | Access to dashboards and systems |
| Cloud infrastructure (AWS) | Hosts all systems and data |
| API connections | Link Helios to vendors and other systems |

---

## 3. Threat Actors

| Threat actor | Example attacks | Likely impact |
|--------------|-----------------|---------------|
| Cybercriminals | Phishing, ransomware | Data loss, downtime |
| Nation-state actors | Attacks on energy infrastructure | Energy disruption |
| Insiders | Misuse of access | Data leaks, data loss |
| Hacktivists | Defacement, data exposure | Reputation damage |

---

## 4. Risk Register

| ID | Risk | Vulnerability (assumed) | Threat actor | L | I | Score | Rating |
|----|------|-------------------------|--------------|---|---|-------|--------|
| R1 | Stolen credentials give unauthorized access to Helios energy data | Password-only login on some accounts; credentials reused | Cybercriminals | 4 | 4 | 16 | High |
| R2 | Ransomware encrypts cloud databases and workloads | Backups not isolated or regularly restore-tested | Cybercriminals | 3 | 5 | 15 | High |
| R3 | Vendor or API compromise exposes data through a third party | Vendors not consistently reviewed; broad API access | Cybercriminals, nation-state | 3 | 4 | 12 | High |
| R4 | Phishing leads to employee account takeover | Limited training; email authentication not fully enforced | Cybercriminals | 4 | 4 | 16 | High |
| R5 | Insider misuses or deletes operational data | Broad database permissions; limited activity logging | Insiders | 2 | 4 | 8 | Medium |
| R6 | Nation-state attack disrupts visibility into energy operations | Limited segmentation between Helios and site systems (assumption) | Nation-state | 2 | 5 | 10 | High |
| R7 | Cloud misconfiguration exposes data or services | Shared responsibility for AWS not fully owned internally | Any | 3 | 4 | 12 | High |
| R8 | Sensitive data exposed or intercepted | Inconsistent encryption and data classification | Cybercriminals, insiders | 2 | 3 | 6 | Medium |
| R9 | Hacktivists deface or disrupt public-facing services | Public endpoints without DDoS or web application protection | Hacktivists | 3 | 2 | 6 | Medium |

*L = Likelihood (1-5), I = Impact (1-5).*

---

## 5. Treatment Plan and Framework Mapping

| ID | Controls | NIST CSF 2.0 | ISO/IEC 27001:2022 Annex A | Treatment | Owner (role) | Residual (L x I) |
|----|----------|--------------|----------------------------|-----------|--------------|------------------|
| R1 | Phishing-resistant MFA; role-based access control; alerts on abnormal logins | PR.AA, DE.CM | A.5.15, A.5.17, A.8.5, A.8.16 | Mitigate | Head of IT Security | 2 x 4 = 8 (Medium) |
| R2 | Immutable and offline backups; regular restore tests; least-privilege database access; logging and workload protection; incident response plan | PR.DS, PR.IR, RC.RP, RS.MA | A.8.13, A.8.7, A.8.15, A.5.26, A.5.30 | Mitigate and transfer (cyber insurance) | Cloud Platform Lead | 2 x 3 = 6 (Medium) |
| R3 | Vendor security review (SOC 2 report, questionnaire); breach-notification clauses in contracts; API authentication and rate limits | GV.SC, PR.AA | A.5.19, A.5.20, A.5.21, A.5.22 | Mitigate | Vendor Risk / Procurement | 2 x 3 = 6 (Medium) |
| R4 | Security awareness and phishing simulations; SPF, DKIM, and DMARC enforcement; phishing-resistant MFA | PR.AT, PR.AA | A.6.3, A.5.14, A.8.5 | Mitigate | Head of IT Security | 3 x 3 = 9 (Medium) |
| R5 | Restricted database permissions; separation of duties; access logging; prompt offboarding | PR.AA, DE.CM | A.8.3, A.8.2, A.8.15, A.6.5 | Mitigate | IT Security and HR | 2 x 3 = 6 (Medium) |
| R6 | Network segmentation; threat intelligence feeds; continuous monitoring; tested incident response and recovery plans | ID.RA, DE.CM, PR.IR, RS.MA | A.5.7, A.8.22, A.8.16, A.5.24 | Mitigate | Head of IT Security | 2 x 4 = 8 (Medium) |
| R7 | Secure configuration baselines; cloud posture monitoring; least-privilege IAM; clear shared-responsibility ownership | PR.PS, GV.RR, ID.RA | A.5.23, A.8.9, A.8.2 | Mitigate | Cloud Platform Lead | 2 x 3 = 6 (Medium) |
| R8 | Encryption at rest and in transit (TLS); data classification; access limits on confidential reports | PR.DS | A.8.24, A.5.12, A.5.13, A.5.34 | Mitigate | Data Owner and IT Security | 1 x 3 = 3 (Low) |
| R9 | DDoS and web application protection; minimize public exposure; communications plan for incidents | PR.IR, DE.CM | A.8.20, A.8.21, A.5.26 | Mitigate; accept residual | Cloud Platform Lead | 2 x 2 = 4 (Low) |

---

## 6. Connecting Security Domains to the Technology Stack

Mapping domains to the layers of the stack shows *where* each control belongs, so protection is placed where the risk lives.

| Security domain | Stack layer | Risk | Control | CSF 2.0 |
|-----------------|-------------|------|---------|---------|
| Insider threat | User interface (dashboards) | Unauthorized employee access | Role-based access control (IAM) | PR.AA |
| Insider threat | Database | Data misuse or deletion | Restricted database permissions | PR.AA |
| Third-party risk | APIs / middleware | Vendor compromise | API authentication and access limits | GV.SC |
| Third-party risk | Cloud infrastructure (AWS) | Weak vendor security | Vendor security review and compliance checks | GV.SC |
| Threat intelligence | User logins | Suspicious login activity | Alerting on abnormal login attempts | DE.CM |
| Threat intelligence | Operating system | Malicious processes | System activity monitoring | DE.CM |
| Privacy | Database | Exposure of sensitive data | Encryption at rest | PR.DS |
| Privacy | Network connections | Data interception | Encrypted connections (HTTPS/TLS) | PR.DS |

---

## 7. Recommendations

**First 30 days:** Enforce MFA for all Helios and AWS access, enable DMARC enforcement, and verify that backups are isolated and can actually be restored.

**Next 90 days:** Complete vendor reviews for every integration with data access, tighten database and IAM permissions, and establish logging and alerting for abnormal logins and API activity.

**Ongoing:** Run phishing simulations, test the incident response plan at least annually, review the risk register quarterly, and revisit scores as the environment changes.

---

## Frameworks Referenced

- NIST Cybersecurity Framework (CSF) 2.0
- ISO/IEC 27001:2022, Annex A

*Framework mappings are illustrative. Verify control references against the official standards before relying on them.*
