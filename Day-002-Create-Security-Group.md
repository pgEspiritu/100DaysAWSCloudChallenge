# 🚀 AWS Incremental Migration Task  
## 🔐 Create a Security Group in Default VPC (us-east-1)

---

## 🧩 Problem Overview

The **Nautilus DevOps Team** is migrating part of their infrastructure to **:contentReference[oaicite:0]{index=0} (AWS)** using an **incremental migration approach**.  
By dividing the migration into smaller tasks, the team ensures:

- Better operational control  
- Reduced risk during changes  
- Minimal service disruption  
- Optimized use of cloud resources  

---

## 🎯 Task Objective

Create a **Security Group** under the **default VPC** with the following specifications:

| Requirement | Value |
|------------|------|
| **Security Group Name** | `datacenter-sg` |
| **Description** | `Security group for Nautilus App Servers` |
| **VPC** | Default VPC |
| **Inbound Rule 1** | HTTP, Port 80, Source `0.0.0.0/0` |
| **Inbound Rule 2** | SSH, Port 22, Source `0.0.0.0/0` |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ **Important:** Credentials are **temporary** and valid only during the given window.

| Field | Value |
|------|------|
| **Console URL** | https://144119524572.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_819180` |
| **Password** | `45dGPxB!nNi@` |
| **Start Time** | Mon Feb 23 23:24:01 UTC 2026 |
| **End Time** | Tue Feb 24 00:24:01 UTC 2026 |

---

## 🛠️ Solution — Using AWS Management Console (Preferred)

### Step 1️⃣: Log in to AWS Console
1. Open the **Console URL** provided above.
2. Log in using the given **username** and **password**.
3. Ensure login is successful.

---

### Step 2️⃣: Confirm the AWS Region
1. Check the **region selector** in the top-right corner.
2. Ensure it is set to:
```text
us-east-1 (N. Virginia)
```

> ⚠️ Switch to **us-east-1** if a different region is selected.

---

### Step 3️⃣: Navigate to EC2 Service
1. From the AWS Console homepage, search for **EC2**.
2. Click **EC2** to open the EC2 Dashboard.

---

### Step 4️⃣: Open Security Groups
1. In the left-hand navigation pane, scroll to **Network & Security**.
2. Click **Security Groups**.

---

### Step 5️⃣: Create the Security Group
1. Click **Create security group**.
2. Fill in the following details:

| Field | Value |
|-----|------|
| **Security group name** | `datacenter-sg` |
| **Description** | `Security group for Nautilus App Servers` |
| **VPC** | Default VPC |

---

### Step 6️⃣: Configure Inbound Rules

#### 🔓 Inbound Rule 1 — HTTP
| Setting | Value |
|------|------|
| **Type** | HTTP |
| **Protocol** | TCP |
| **Port Range** | 80 |
| **Source** | `0.0.0.0/0` |

#### 🔐 Inbound Rule 2 — SSH
| Setting | Value |
|------|------|
| **Type** | SSH |
| **Protocol** | TCP |
| **Port Range** | 22 |
| **Source** | `0.0.0.0/0` |

> Leave **Outbound rules** as default (Allow all traffic).

---

### Step 7️⃣: Create the Security Group
1. Review all configurations.
2. Click **Create security group**.

---

### Step 8️⃣: Verify Security Group Creation
1. Confirm that `datacenter-sg` appears in the **Security Groups** list.
2. Validate:
   - VPC: Default VPC  
   - Inbound rules: HTTP (80) and SSH (22)  
   - Source: `0.0.0.0/0`
3. Or by using KodeKloud CLI:
```bash
aws ec2 describe-security-groups --group-names datacenter-sg
```
---

## ✅ Final Validation Checklist

- [x] Security group name is `datacenter-sg`  
- [x] Description is correct  
- [x] Created under **default VPC**  
- [x] HTTP (80) inbound rule added  
- [x] SSH (22) inbound rule added  
- [x] Region is **us-east-1**

---

## 🎉 Task Completed Successfully!

The security group required for the Nautilus DevOps team’s incremental AWS migration has been created successfully and is ready to be attached to EC2 instances for application and administrative access.

---
