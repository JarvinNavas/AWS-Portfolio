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
