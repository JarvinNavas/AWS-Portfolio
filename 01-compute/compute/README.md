# Lab: Deploying a Web Server on EC2 with User Data

## 📌 Project Overview
While S3 is perfect for static content, dynamic applications require compute power. In this lab, I provisioned a virtual server using **Amazon EC2**, configured network security, and automated the software installation process using a **Bootstrapping** script.

## 🎯 Business Goals
1.  **Agility:** rapidly deploy compute resources without hardware procurement.
2.  **Automation:** Reduce human error by automating the installation of the web server (Infrastructure as Code principles).
3.  **Security:** Implement a firewall (Security Group) that follows the principle of least privilege.

## 🛠️ Architecture & Services
* **Amazon EC2 (Elastic Compute Cloud):** The virtual server (t2.micro/t3.micro).
* **Security Groups:** Acts as a virtual firewall to control inbound traffic.
* **User Data:** A script passed to the instance at launch time to perform automated configuration.

## 🚀 Implementation Steps

### 1. Instance Provisioning
Launched an Amazon Linux 2023 instance within the Free Tier limits.
* **Key Pair:** Created an RSA key pair for secure SSH access.

### 2. Network Security (Security Groups)
Configured a Security Group to filter traffic:
* **Port 22 (SSH):** Restricted to my personal IP address for administration.
* **Port 80 (HTTP):** Open to `0.0.0.0/0` (Anywhere) to serve web traffic to users.

![Security Group Config](screenshots/ec2-security-group.png)
*(Screenshot of the Network Settings showing allowed ports)*

### 3. Bootstrapping (User Data)
Instead of manually installing software, I injected a Bash script into the **User Data** field. This script ran automatically upon first boot to:
1.  Update system packages.
2.  Install the Apache Web Server (`httpd`).
3.  Start and enable the service.
4.  Deploy a custom HTML landing page.

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Automated Setup</h1>" > /var/www/html/index.html
