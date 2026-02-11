# Phase 2 - Module 01: IAM Advanced Policy (MFA Enforcement) 🛡️

## 📋 Scenario
Standard IAM policies often allow destructive actions (like `DeleteObject`) based solely on user identity. If credentials are compromised, attackers can wipe critical data. In this module, I implemented a **Zero Trust** approach using **IAM Condition Keys** to enforce Multi-Factor Authentication for sensitive operations.

## 🎯 Objectives
* **Enforce MFA:** Deny destructive actions (Delete) unless the session is authenticated with a valid MFA token.
* **Explicit Deny Logic:** Use the `Deny` effect with the `aws:MultiFactorAuthPresent` condition to override any existing allow permissions.

## ⚙️ Implementation Details

### 1. The JSON Policy Strategy
I created a custom customer-managed policy (`S3-Hardened-MFA-Policy`) acting as a guardrail. It allows normal S3 operations but explicitly denies deletion if MFA is not present.

**The Policy Logic:**

```json
{
    "Sid": "DenyDeleteWithoutMFA",
    "Effect": "Deny",
    "Action": "s3:DeleteObject",
    "Resource": "*",
    "Condition": {
        "BoolIfExists": {
            "aws:MultiFactorAuthPresent": "false"
        }
    }
}
2. Evidence of Protection (Blocked Attempt)
First, I attempted to delete a file using valid user credentials but without an active MFA session token. The policy correctly triggered an Access Denied error, blocking the potential threat.

3. Successful Validation (Authorized Access)
After authenticating with the MFA device (updating the session token), the condition aws:MultiFactorAuthPresent became "true", and the deletion was permitted.

🛡️ Value Added
This configuration ensures that even if an attacker steals long-term credentials (password or access keys), they cannot perform irreversible actions like data deletion without physical access to the MFA device.

Module completed by: Jarvin Navas
