# Phase 2 - Module 01: IAM Advanced Policy (MFA Enforcement) 🛡️

## 📋 Scenario
Standard IAM policies often allow destructive actions (like `DeleteObject`) based solely on user identity. If credentials are compromised, attackers can wipe data.
In this module, I implemented a **Zero Trust** approach using **IAM Condition Keys**.

## 🎯 Objectives
* **Enforce MFA:** Deny destructive actions (Delete) unless the session is authenticated with Multi-Factor Authentication.
* **Explicit Deny Logic:** Use the `Deny` effect with the `aws:MultiFactorAuthPresent` condition to override any existing permissions.

## ⚙️ Implementation Details

### 1. The JSON Policy Strategy
I created a custom customer-managed policy (`S3-Hardened-MFA-Policy`) with the following logic:
* **Allow:** Read/Write access to S3.
* **Deny:** `s3:DeleteObject` IF `aws:MultiFactorAuthPresent` is `false`.

```json
"Condition": {
    "BoolIfExists": {
        "aws:MultiFactorAuthPresent": "false"
    }
}
2. Evidence of Protection
First, I attempted to delete a file using valid credentials but without an active MFA session token. AWS correctly blocked the request.

3. Successful Validation
After authenticating with the MFA device (updating the session token), the Condition was satisfied, and the deletion was permitted.

🛡️ Value Added
This configuration ensures that even if an attacker steals long-term credentials (password or access keys), they cannot perform irreversible actions without physical access to the MFA device.

Module completed by: Jarvin Navas
