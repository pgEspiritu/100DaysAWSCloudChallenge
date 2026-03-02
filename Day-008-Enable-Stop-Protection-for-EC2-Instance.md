# 🚀 AWS EC2 Protection Task  
## 🔒 Enable Stop Protection for an EC2 Instance (us-east-1)

---

## 🧩 Problem Overview

During the AWS migration process, the Nautilus DevOps team deployed several resources.  
One EC2 instance now requires **stop protection** to prevent accidental shutdowns during operations.

**Stop protection** ensures that an EC2 instance cannot be stopped accidentally from the console, CLI, or automation scripts.

---

## 🎯 Task Objective

Enable **Stop Protection** for the following instance:

| Requirement | Value |
|------------|------|
| **Instance Name** | `xfusion-ec2` |
| **Feature** | Stop Protection |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

> ⚠️ Credentials are temporary and valid only during the specified window.

| Field | Value |
|------|------|
| **Console URL** | https://717740812428.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_889126` |
| **Password** | `DUCTZSrdD71e` |
| **Start Time** | Mon Mar 02 12:25:37 UTC 2026 |
| **End Time** | Mon Mar 02 13:25:37 UTC 2026 |

---

# 🛠️ Solution — Using AWS Management Console (Preferred)


## Step 1️⃣: Log in to AWS Console

1. Open the provided **Console URL**.
2. Sign in using the given username and password.
3. Confirm successful login.

---

## Step 2️⃣: Verify Region

Ensure the region (top-right corner) is set to:
```text
us-east-1 (N. Virginia)
```

---

## Step 3️⃣: Navigate to EC2

1. Search for **EC2** in the AWS Console search bar.
2. Open the EC2 Dashboard.
3. Click **Instances** from the left navigation pane.

---

## Step 4️⃣: Locate the Instance

Find the instance named:
```text
xfusion-ec2
```

Select the checkbox beside the instance.

---

## Step 5️⃣: Enable Stop Protection

1. Click the **Actions** dropdown.
2. Navigate to:
```text
Actions → Instance settings → Change stop protection
```

3. In the dialog box:
   - ✅ Enable **Stop protection**
4. Click **Save** or **Apply**.

---

## Step 6️⃣: Verify Stop Protection

1. Select the instance again.
2. Open the **Details** tab.
3. Confirm:
```text
Stop protection: Enabled
```

---

## ✅ Final Validation Checklist

- [x] Instance name is `xfusion-ec2`  
- [x] Region is `us-east-1`  
- [x] Stop protection enabled successfully  
- [x] Instance cannot be stopped accidentally  

---

## 🎉 Task Completed Successfully!

Stop protection has been enabled for the EC2 instance **xfusion-ec2**, safeguarding it against unintended shutdowns during the ongoing AWS migration activities.

---
