# 🚀 AWS Incremental Migration Task
## 🔐 Create an EC2 Key Pair via **AWS CLI** (us-east-1)

---

## 🧩 Problem Overview

The **Nautilus DevOps Team** is migrating part of their infrastructure to **Amazon Web Services (AWS)** using an **incremental migration strategy**.

Instead of performing one large migration, tasks are completed in smaller phases to:

- Reduce operational and security risks  
- Maintain better visibility and control  
- Minimize disruption to live services  
- Optimize cloud resource usage  

---

## 🎯 Task Objective

Create an **EC2 Key Pair** with the following specifications:

| Requirement | Value |
|------------|------|
| Key Pair Name | `nautilus-kp` |
| Key Pair Type | RSA |
| Region | `us-east-1` |
| Method | AWS CLI (KodeKloud Terminal) |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ **Important:** Credentials are temporary and expire after the lab window.

| Field | Value |
|------|------|
| Console URL | https://447205410565.signin.aws.amazon.com/console?region=us-east-1 |
| Username | kk_labs_user_383625 |
| Password | AvsxB4lTh8Xn |
| Start Time | Sun Feb 22 23:25:53 UTC 2026 |
| End Time | Mon Feb 23 00:25:53 UTC 2026 |

---

# 🛠️ Solution — AWS CLI (KodeKloud Terminal)

---

## Step 1️⃣: Retrieve AWS Credentials

On the **aws-client / KodeKloud terminal**, run:

```bash
showcreds
```

Example output:
```bash
AWS_ACCESS_KEY_ID=XXXXXXXX
AWS_SECRET_ACCESS_KEY=XXXXXXXX
AWS_DEFAULT_REGION=us-east-1
```

---

## Step 2️⃣: Configure AWS CLI

Configure AWS CLI using the retrieved credentials:
```bash
aws configure
```

Enter the values:
```bash
AWS Access Key ID: <ACCESS_KEY>
AWS Secret Access Key: <SECRET_KEY>
Default region name: us-east-1
Default output format: json
```

---

## Step 3️⃣: Verify AWS CLI Configuration
```bash
aws sts get-caller-identity
```
✅ Expected result: Account and user details are displayed.

---

## Step 4️⃣: Create the EC2 Key Pair (RSA)

Run the following command:
```bash
aws ec2 create-key-pair \
    --key-name nautilus-kp \
    --key-type rsa \
    --region us-east-1 \
    --query "KeyMaterial" \
    --output text > nautilus-kp.pem
```

---

## Step 5️⃣: Secure the Private Key

Set proper permissions (required for SSH usage):
```bash
chmod 400 nautilus-kp.pem
```
✅ This ensures only the owner can read the key.

---

## Step 6️⃣: Verify Key Pair Creation

List available key pairs:
```bash
aws ec2 describe-key-pairs --region us-east-1
```

Expected output should include:
```bash
KeyName: nautilus-kp
KeyType: rsa
```

---

## Step 7️⃣: Confirm Local Key File

Verify the key file exists:
```bash
ls -l nautilus-kp.pem
```

Expected:
```bash
-r-------- nautilus-kp.pem
```

---

## ✅ Final Validation Checklist

- Key pair name is nautilus-kp
- Key type is RSA
- Created in us-east-1 region
- Private key downloaded locally
- Proper file permissions applied (chmod 400)


