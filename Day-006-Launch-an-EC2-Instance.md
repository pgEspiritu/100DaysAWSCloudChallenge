# 🚀 AWS Incremental Migration Task  
## 🖥️ Launch an EC2 Instance (us-east-1)

---

## 🧩 Problem Overview

The **Nautilus DevOps Team** is executing an incremental migration to **(AWS)**.  
To support this phase, an EC2 instance must be launched with specific configuration requirements.

---

## 🎯 Task Objective

Create an EC2 instance with the following specifications:

| Requirement | Value |
|------------|------|
| **Instance Name** | `devops-ec2` |
| **AMI** | Amazon Linux |
| **Instance Type** | `t2.micro` |
| **Key Pair** | Create new RSA key pair named `devops-kp` |
| **Security Group** | Default security group |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ These credentials are temporary and time-bound.

| Field | Value |
|------|------|
| **Console URL** | https://467239208986.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_301802` |
| **Password** | `kD3u!q!N@l%B` |
| **Start Time** | Sat Feb 28 00:59:18 UTC 2026 |
| **End Time** | Sat Feb 28 01:59:18 UTC 2026 |

---

# 🛠️ Solution — Using AWS Management Console (Preferred)

## Step 1️⃣: Log in to AWS Console

1. Open the provided **Console URL**.
2. Enter the given username and password.
3. Confirm successful login.

---

## Step 2️⃣: Verify AWS Region

Ensure the region (top-right corner) is:
```text
us-east-1 (N. Virginia)
```

> ⚠️ Switch to **us-east-1** if needed.

---

## Step 3️⃣: Navigate to EC2

1. From the AWS Console homepage, search for **EC2**.
2. Open the EC2 Dashboard.
3. Click **Launch instance**.

---

## Step 4️⃣: Configure Basic Details

### 🏷️ Name and Tags
- **Name:** `devops-ec2`

---

## Step 5️⃣: Choose Amazon Machine Image (AMI)

1. Under **Application and OS Images**, select:
   - **Amazon Linux (latest available version)**

> Typically labeled as **Amazon Linux 2 AMI** or **Amazon Linux 2023**.

---

## Step 6️⃣: Choose Instance Type

- Select:
```text
t2.micro
```

> ✔️ Eligible for Free Tier (if applicable)

---

## Step 7️⃣: Create New RSA Key Pair

Under **Key pair (login)**:

1. Click **Create new key pair**
2. Enter:
   - **Key pair name:** `devops-kp`
   - **Key pair type:** `RSA`
   - **Private key format:** `.pem`
3. Click **Create key pair**
4. Save the downloaded file securely.

> ⚠️ AWS does NOT allow re-downloading private keys.

---

## Step 8️⃣: Configure Network Settings

1. Leave **VPC** as default.
2. Select the **default security group** (already available by default).
3. Do not create a new security group.

---

## Step 9️⃣: Review and Launch

1. Review all configuration settings.
2. Click **Launch instance**.

---

## Step 🔟: Verify Instance

1. Go to **EC2 → Instances**
2. Confirm:

| Setting | Expected Value |
|----------|----------------|
| Name | `devops-ec2` |
| Instance Type | `t2.micro` |
| AMI | Amazon Linux |
| Key Pair | `devops-kp` |
| Security Group | default |
| State | Running |

---

# ✅ Final Validation Checklist

- [x] Instance name is `devops-ec2`  
- [x] AMI is Amazon Linux  
- [x] Instance type is `t2.micro`  
- [x] RSA key pair `devops-kp` created  
- [x] Default security group attached  
- [x] Region is `us-east-1`  
- [x] Instance state is **Running**

---

# 🎉 Task Completed Successfully!

The EC2 instance has been successfully launched and is ready for use in the Nautilus DevOps team's phased AWS migration process.

---
