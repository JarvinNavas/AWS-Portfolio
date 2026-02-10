# Module 02: Secure Storage & Ransomware Protection (S3) 🗄️

## 📋 Overview
This module focuses on creating a **Resilient Storage Layer** for critical audit logs. The architecture prioritizes data immutability to withstand ransomware attacks and insider threats, ensuring that forensic evidence remains intact even if the root account is compromised.

## 🎯 Objectives
* **Data Immutability (WORM):** prevent log deletion or modification for a specific retention period.
* **Data Integrity:** Ensure that accidental deletions can be reversed.
* **Confidentiality:** Enforce encryption at rest and block all unauthorized public access paths.

## 🛠️ Implementation Details

### 1. Object Lock & Compliance (WORM Model)
I implemented AWS S3 Object Lock to enforce a "Write Once, Read Many" model.
* **Mode:** Governance Mode.
* **Retention Period:** 1 Day (Pilot phase).
* **Impact:** Objects committed to this bucket cannot be overwritten or deleted by any user (including the root user, unless specific bypass permissions are used) for 24 hours. This creates a safe buffer for incident response.
* *Evidence:* `evidence/object-lock-retention-rules.`

### 2. Perimeter Security (Block Public Access)
I enabled the "Block Public Access" setting at the bucket level.
* **ACLs:** Disabled (Modern approach).
* **Policy:** All public access points (new and existing) are blocked.
* *Evidence:* `evidence/block-public-access`

### 3. Data Resilience Features
* **Versioning:** Enabled. Acts as a backup mechanism for accidental deletions.
* **Server-Side Encryption (SSE-S3):** All data is automatically encrypted at rest using AES-256 managed keys.

---
*Module completed by: Jarvin Navas*
