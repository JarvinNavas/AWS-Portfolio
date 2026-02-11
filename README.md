# AWS Cloud Security & automated Incident Response (SOAR) 🛡️

**Role:** Cloud Security Engineer / Blue Team
**Tech Stack:** AWS (IAM, S3, GuardDuty, Lambda, CloudTrail), Python (Boto3), Terraform concept.

## 🚀 Project Executive Summary
This repository documents the implementation of a **Defense-in-Depth** architecture on AWS. The project simulates a real-world scenario where I built a secure infrastructure from scratch, implementing controls for **Identity (IAM)**, **Data Protection (S3)**, **Monitoring (CloudWatch)**, and **Automated Response (Lambda/SOAR)**.

## 🗺️ Architecture Roadmap

| Day | Module | Key Technologies | Outcome |
| :--- | :--- | :--- | :--- |
| **01** | [Identity Hardening](./01-identity-access-management) | IAM, MFA, RBAC | Eliminated Root usage & enforced Least Privilege. |
| **02** | [Ransomware Protection](./02-secure-storage-s3) | S3 Object Lock, KMS | Created an immutable WORM vault for audit logs. |
| **03** | [Forensic Logging](./03-logging-auditing) | CloudTrail | Enabled full visibility of API activity for auditing. |
| **04** | [Threat Detection](./04-monitoring-alerting) | CloudWatch, SNS | Configured real-time alerts for Brute Force attacks. |
| **05** | [Network Defense](./05-network-security) | VPC, Security Groups | Designed a segmented network & hardened firewalls. |
| **06** | [Automated Response (SOAR)](./06-incident-response) | Lambda, Python (Boto3) | Developed a "Kill Switch" robot to block attackers instantly. |
| **07** | [Compliance Audit](./07-compliance-audit) | Trusted Advisor | Validated security posture against CIS Benchmarks. |

## 💡 Key Competencies Demonstrated

### 🔐 Identity & Access Management (IAM)
* Implementation of **RBAC** (Role-Based Access Control).
* Enforcement of **MFA** and strong password policies.
* **Least Privilege** application in JSON policies.

### 👁️ Security Operations (SecOps)
* **Continuous Monitoring:** Transformation of passive logs into active alerts.
* **Incident Response:** Automated remediation of security groups using **Python (Boto3)**.
* **Forensics:** Chain of custody preservation using S3 Versioning and Object Lock.

### ☁️ Cloud Architecture
* **VPC Design:** Public/Private subnet segmentation.
* **Infrastructure as Code:** Management of security rules via scriptable interfaces.

---
*This portfolio demonstrates the ability to secure cloud environments proactively and reactively.*
