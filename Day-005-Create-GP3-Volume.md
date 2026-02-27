# 🚀 AWS Incremental Migration Task  
## 💾 Create an EBS Volume (us-east-1)

---

## 🧩 Problem Overview

The **Nautilus DevOps Team** is performing an incremental migration to (AWS)**.  

As part of this phased migration, a new **Elastic Block Store (EBS) volume** must be created to support application or infrastructure workloads.

This ensures:
- Flexible storage provisioning  
- Independent lifecycle management  
- Scalable and high-performance block storage  

---

## 🎯 Task Objective

Create an **EBS Volume** with the following specifications:

| Requirement | Value |
|------------|------|
| **Volume Name** | `datacenter-volume` |
| **Volume Type** | `gp3` |
| **Volume Size** | 2 GiB |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ **Important:** Credentials are temporary and valid only within the specified time window.

| Field | Value |
|------|------|
| **Console URL** | https://915501509755.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_998493` |
| **Password** | `Q5toE3aaqR@^` |
| **Start Time** | Fri Feb 27 12:11:48 UTC 2026 |
| **End Time** | Fri Feb 27 13:11:48 UTC 2026 |

---

## 🛠️ Solution — Using AWS Management Console (Preferred)

### Step 1️⃣: Log in to AWS Console
1. Open the provided **Console URL**.
2. Log in using the supplied **username** and **password**.
3. Confirm successful login.

---

### Step 2️⃣: Verify Region
1. Check the region selector in the top-right corner.
2. Ensure it is set to:
```text
us-east-1 (N. Virginia)
```

> ⚠️ If not, switch to **us-east-1**.

---

### Step 3️⃣: Navigate to EC2 Service
1. From the AWS Console homepage, search for **EC2**.
2. Click **EC2** to open the EC2 Dashboard.

---

### Step 4️⃣: Open Volumes Section
1. In the left-hand navigation pane, scroll to **Elastic Block Store**.
2. Click **Volumes**.
3. Click **Create volume**.

---

### Step 5️⃣: Configure Volume Settings

Fill in the following:

| Field | Value |
|------|------|
| **Volume type** | `gp3` |
| **Size (GiB)** | `2` |
| **Availability Zone** | Any in `us-east-1` (e.g., `us-east-1a`) |

> ⚠️ The Availability Zone must match where the volume will eventually be attached (if needed).

---

### Step 6️⃣: Add Name Tag
1. Expand the **Tags** section.
2. Click **Add tag**.
3. Enter:

| Key | Value |
|-----|------|
| `Name` | `datacenter-volume` |

---

### Step 7️⃣: Create the Volume
1. Review all configurations.
2. Click **Create volume**.

---

### Step 8️⃣: Verify Volume Creation
1. Confirm that the volume appears in the **Volumes** list.
2. Validate:
   - **Type:** gp3  
   - **Size:** 2 GiB  
   - **State:** Available  
   - **Tag Name:** datacenter-volume  

3. Or Verify using CLI
```bash
aws ec2 describe-volumes \
    --region us-east-1 \
    --filters Name=volume-type,Values=gp3 \
    --query "Volumes[*].[Name,VolumeId,Size,State,AvailabilityZone]" \
    --output table
```

---

## ✅ Final Validation Checklist

- [x] Volume name tag is `datacenter-volume`  
- [x] Volume type is **gp3**  
- [x] Size is **2 GiB**  
- [x] Created in **us-east-1**  
- [x] Volume state is **Available**  

---

## 🎉 Task Completed Successfully!

The required EBS volume has been successfully created and is ready to be attached to an EC2 instance as part of the Nautilus DevOps team’s incremental AWS migration process.

---
