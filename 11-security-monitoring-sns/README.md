# Module 11: Security Monitoring & Threat Hunting (SOC) 🚨

## 📋 Scenario
A foundational rule of Cloud Security is that the AWS Root account must never be used for daily tasks. If a login event occurs using the Root credentials, it indicates either a severe policy violation by an internal employee or an active compromise by an external threat actor. 

## 🎯 Objectives
* **Automated Alerting:** Configure EventBridge and SNS to route critical security events to an incident response team.
* **Threat Hunting:** Manually audit and query AWS CloudTrail to track down specific unauthorized access events when automated systems experience delays or filter drops.

## ⚙️ Implementation Details & Evidence

### 1. The Detection Logic (Amazon EventBridge & SNS)
I deployed an EventBridge Rule configured with a custom JSON event pattern to act as a tripwire, filtering API calls for `"userIdentity": {"type": ["Root"]}` and pushing them to an SNS topic.

### 2. Forensic Auditing (AWS CloudTrail)
To validate the security posture and perform active Threat Hunting, I bypassed the automated alerting systems and queried the master API logs directly in **AWS CloudTrail**. 
By filtering the management events for `Event name: ConsoleLogin`, I successfully isolated and identified the exact timestamps and source IPs of the Root user login events, proving the ability to trace an attacker's steps natively.

![CloudTrail Root Login Audit](evidence/cloudtrail-root-login.png)

## 🛡️ Value Added
* **Forensic Capabilities:** Demonstrates the ability to perform root-cause analysis and forensic investigations post-incident.
* **Defense in Depth:** Combines automated tripwires with manual auditing skills, forming the foundation of a modern SOC (Security Operations Center) analyst.

---
*Module completed by: Jarvin Navas*
