# Module 15: Secure Serverless Web Portfolio (S3 + CloudFront)

## 🎯 Objective
Deploy a highly available, globally distributed, and secure static website using a Serverless architecture on AWS. This project serves as my professional Cloud Cybersecurity portfolio, demonstrating the transition from traditional server-based hosting to a modernized, zero-maintenance edge architecture.

## 🔗 Live Demo
**URL:** [https://d1f19tjig5u0p6.cloudfront.net](https://d1f19tjig5u0p6.cloudfront.net) *(Live Serverless Portfolio)*

## 🏗️ Architecture & Services Used
* **Amazon S3 (Simple Storage Service):** Configured as a static website host to serve HTML/CSS assets without the need for underlying EC2 instances (Serverless).
* **AWS IAM (Resource-based Policies):** Implemented a strict Bucket Policy to allow public `s3:GetObject` actions only for web delivery.
* **Amazon CloudFront (CDN):** Distributed the website globally across AWS Edge Locations to ensure ultra-low latency. 
* **Security & Encryption:** Enforced **HTTPS (TLS encryption)** at the CloudFront layer, automatically redirecting all insecure HTTP traffic to HTTPS to protect data in transit.

## 🛡️ Cybersecurity Focus
While a standard S3 website operates over HTTP, deploying it behind CloudFront is a critical security best practice. It mitigates direct exposure of the S3 bucket, protects against basic DDoS attempts at the edge layer, and ensures all client-server communication is encrypted.

## 📝 Steps Performed (ClickOps / Manual)
1. Created an S3 bucket with a globally unique name.
2. Uploaded the portfolio code (`index.html`).
3. Enabled "Static Website Hosting" on the S3 bucket.
4. Modified the S3 Block Public Access settings and applied a custom JSON Bucket Policy for public read access.
5. Provisioned a CloudFront Distribution pointing to the S3 website endpoint.
6. Configured the CloudFront Viewer Protocol Policy to `Redirect HTTP to HTTPS`.
