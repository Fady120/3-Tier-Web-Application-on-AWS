# 🏗️ 3‑Tier Web Application on AWS


## Table of Contents 📘

- [Solution Overview](#solution-overview)  
- [Architecture Diagram](#architecture-diagram)  
- [Components](#components)  
  - [Networking 🚦](#networking)  
  - [Security 🔒](#security)  
  - [Frontend Tier 🌐](#frontend-tier)  
  - [Backend Tier ⚙️](#backend-tier)  
  - [Database Tier 🗄️](#database-tier)  
  - [Monitoring & Logging 📊](#monitoring--logging)  
- [Manual Deployment Steps](#manual-deployment-steps)  
- [Use Cases & Benefits](#use-cases--benefits)  
- [Customization](#customization)  
- [Cleanup 🧹](#cleanup)

---

## Solution Overview ✨

This repository illustrates how to manually provision a **highly available**, **scalable**, and **secure 3‑tier web application** on AWS using the AWS Console or CLI.  
Ideal for learning cloud architecture, auditing infrastructure, or environments where scripted automation isn't used.

---

## Architecture Diagram 🖼️

Below is the high-level architecture deployed across two Availability Zones:

![Architecture Diagram](Architecture.gif)

---

## Components ⚙️

### Networking 🚦
- VPC with two **public** and two **private** subnets  
- **Internet Gateway** for inbound traffic  
- **NAT Gateways** for secure egress  
- Custom **Route Tables** ensuring proper routing

### Security 🔒
- **Security Groups** segmented for frontend, backend, and database  
- **WAF** protections at edge (CloudFront) and application layers  
- **IAM Roles** with least-privilege access for EC2

### Frontend Tier 🌐
- Public EC2 instances running NGINX  
- **Auto Scaling Group** for capacity management  
- **Internet-facing ALB** to distribute traffic  
- **CloudFront** for caching, edge delivery, and DDoS protection

### Backend Tier ⚙️
- Private EC2 instances serving application/API  
- **Internal Load Balancer** for service-to-service traffic  
- Secure communication with frontend and database tiers

### Database Tier 🗄️
- **Amazon RDS** (PostgreSQL/MySQL) in Multi‑AZ setup  
- Automated backups, snapshots, and failover  
- Access restricted to backend instances only

### Monitoring & Logging 📊
- **Amazon CloudWatch** collects metrics and logs  
- Alarms monitor unhealthy instances or thresholds  
- Optional **SNS** integration for alerts

---

## Manual Deployment Steps 📋

1. **Network Setup** 🚧  
2. **Security Configuration** 🔐  
3. **Deploy Frontend** 🌐  
4. **Deploy Backend** ⚙️  
5. **Provision Database** 🗄️  
6. **Enable Monitoring** 📈

---

## Use Cases & Benefits 💡

- **Hands-on learning** of AWS infrastructure  
- **Audit-friendly** transparent provisioning  
- **Production-grade template** for web/API apps  
- **Cost-conscious**, leveraging AWS free-tier

---

## Customization 🔧

- Swap backend EC2 with **ECS/EKS**  
- Add caching layer: **Redis**, **Memcached**  
- Integrate **CI/CD pipelines** with CodeDeploy/GitHub Actions  
- Export to **CloudFormation** for automation  
- Enhance with **VPC Flow Logs**, advanced **CloudWatch dashboards**, or **AWS X-Ray**

---

## Cleanup 🧹

To avoid ongoing costs, delete resources in this order:

1. CloudFront  
2. Load Balancers  
3. EC2 Auto Scaling Groups  
4. RDS instance  
5. NAT Gateways & VPC  
6. CloudWatch logs and alarms