# 🚀 AWS Incremental Migration Task  
## 🔐 Create an EC2 Key Pair via AWS Console (us-east-1)

---

## 🧩 Problem Overview

The **Nautilus DevOps Team** is migrating a portion of their infrastructure to the **:contentReference[oaicite:0]{index=0} (AWS)** cloud using an **incremental migration strategy**.

Instead of executing one large migration, the team breaks the process into **smaller, manageable tasks** to:

- Reduce operational and security risks  
- Maintain better visibility and control  
- Minimize disruption to live services  
- Optimize cloud resource usage  

---

## 🎯 Task Objective

Create an **EC2 Key Pair** with the following requirements:

| Requirement | Value |
|------------|------|
| **Key Pair Name** | `nautilus-kp` |
| **Key Pair Type** | `RSA` |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ **Important:** Credentials are **temporary** and valid only within the specified window.

| Field | Value |
|------|------|
| **Console URL** | https://447205410565.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_383625` |
| **Password** | `AvsxB4lTh8Xn` |
| **Start Time** | Sun Feb 22 23:25:53 UTC 2026 |
| **End Time** | Mon Feb 23 00:25:53 UTC 2026 |

---

## 🛠️ Solution — AWS Management Console (Preferred)


::contentReference[oaicite:1]{index=1}


### Step 1️⃣: Log in to AWS Console
1. Open the **Console URL** provided above.
2. Enter the **username** and **password**.
3. Sign in successfully.

---

### Step 2️⃣: Confirm the AWS Region
1. Look at the **region selector** in the top-right corner.
2. Ensure the region is set to:
```text
us-east-1 (N. Virginia)
```

> ⚠️ If the region is different, switch to **us-east-1** before proceeding.

---

### Step 3️⃣: Open the EC2 Dashboard
1. From the AWS Console homepage, search for **EC2**.
2. Click **EC2** to open the EC2 service dashboard.

---

### Step 4️⃣: Navigate to Key Pairs
1. In the left navigation pane, scroll to **Network & Security**.
2. Click **Key Pairs**.

---

### Step 5️⃣: Create the Key Pair
1. Click **Create key pair**.
2. Enter the following details:

| Field | Value |
|-----|------|
| **Name** | `nautilus-kp` |
| **Key pair type** | `RSA` |
| **Private key format** | `.pem` (default) |

---

### Step 6️⃣: Download the Private Key
1. Click **Create key pair**.
2. The file `nautilus-kp.pem` will be downloaded automatically.
3. Store the file in a **secure location**.

> ⚠️ **Important:** AWS does **not** allow private keys to be re-downloaded.

---

### Step 7️⃣: Verify Key Pair Creation
1. Ensure `nautilus-kp` appears in the **Key Pairs** list.
2. Confirm:
   - **Type:** RSA  
   - **Status:** Available  

or using CLI in the KodeCloud Terminal:
```bash
aws ec2 describe-key-pairs --region us-east-1
```

---

## ✅ Final Validation Checklist

- [x] Key pair name is `nautilus-kp`  
- [x] Key type is **RSA**  
- [x] Created in **us-east-1** region  
- [x] Private key downloaded and secured  

---

## 🎉 Task Completed Successfully!

The required EC2 key pair has been successfully created using the **AWS Management Console** and is ready to be used in the next phase of the Nautilus DevOps team’s incremental cloud migration.

---
