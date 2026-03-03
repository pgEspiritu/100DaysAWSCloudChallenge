# 🚀 AWS EC2 Optimization Task  
## 🔄 Change Instance Type (us-east-1)

---

## 🧩 Problem Overview

During the AWS migration process, the **Nautilus DevOps Team** identified an underutilized EC2 instance and decided to optimize costs by downsizing it.

The instance `datacenter-ec2` must be resized from:
```text
t2.micro → t2.nano
```


⚠️ Important: Ensure **Status Checks are completed** before making any changes.

---

## 🎯 Task Objective

| Requirement | Value |
|------------|------|
| **Instance Name** | `datacenter-ec2` |
| **Current Type** | `t2.micro` |
| **New Type** | `t2.nano` |
| **Final State** | Running |
| **Region** | `us-east-1` |
| **Method** | AWS Management Console |

---

## 🔑 AWS Credentials (Provided)

| Field | Value |
|------|------|
| **Console URL** | https://678838728594.signin.aws.amazon.com/console?region=us-east-1 |
| **Username** | `kk_labs_user_194324` |
| **Password** | `c%HYR@BrwO9F` |
| **Start Time** | Sun Mar 01 00:41:05 UTC 2026 |
| **End Time** | Sun Mar 01 01:41:05 UTC 2026 |

---

# 🛠️ Solution — Using AWS Management Console (Preferred)

## Step 1️⃣: Log in to AWS Console

1. Open the provided Console URL.
2. Sign in using the given credentials.
3. Confirm successful login.

![Day 7 - Change EC2 Instance Type.1](images/Day-007.1.png)

---

## Step 2️⃣: Verify Region

Ensure the region (top-right corner) is:
```text
us-east-1 (N. Virginia)
```

![Day 7 - Change EC2 Instance Type.2](images/Day-007.2.png)

---

## Step 3️⃣: Navigate to EC2

1. Search for **EC2** in the AWS Console.
2. Open the EC2 Dashboard.
3. Click **Instances** in the left panel.

![Day 7 - Change EC2 Instance Type.3](images/Day-007.3.png)

---

## Step 4️⃣: Locate the Instance

1. Find instance named:
```text
datacenter-ec2
```


2. Click the instance ID to open details.

---

## Step 5️⃣: Verify Status Checks

Under the **Status and alarms** tab:

Ensure:
```text
2/2 checks passed
```

⚠️ If still **Initializing**, wait until checks are completed before proceeding.

![Day 7 - Change EC2 Instance Type.4](images/Day-007.4.png)

---

## Step 6️⃣: Stop the Instance

1. Select the instance.
2. Click **Instance state → Stop instance**.

![Day 7 - Change EC2 Instance Type.5](images/Day-007.5.png)

3. Wait until the instance state shows:
```text
Stopped
```

![Day 7 - Change EC2 Instance Type.6](images/Day-007.6.png)

---

## Step 7️⃣: Change Instance Type

1. With the instance selected, click:
   - **Actions → Instance settings → Change instance type**

![Day 7 - Change EC2 Instance Type.7](images/Day-007.7.png)

2. Select:
```text
t2.nano
```

![Day 7 - Change EC2 Instance Type.8](images/Day-007.8.png)

3. Click **Apply**.

![Day 7 - Change EC2 Instance Type.9](images/Day-007.9.png)

---

## Step 8️⃣: Start the Instance

1. Click **Instance state → Start instance**.

![Day 7 - Change EC2 Instance Type.10](images/Day-007.10.png)

2. Wait until the instance state changes to:
```text
Running
```

![Day 7 - Change EC2 Instance Type.11](images/Day-007.11.png)

3. Or check via CLI
```bash
aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=datacenter-ec2" \
  --query "Reservations[*].Instances[*].[InstanceId,InstanceType]" \
  --output table
```

![Day 7 - Change EC2 Instance Type.12](images/Day-007.12.png)

---

## Step 9️⃣: Final Verification

Confirm the following:

| Setting | Expected Value |
|----------|----------------|
| Name | `datacenter-ec2` |
| Instance Type | `t2.nano` |
| Instance State | Running |
| Status Checks | 2/2 Passed |
| Region | us-east-1 |

---

# ✅ Final Validation Checklist

- [x] Status checks completed before modification  
- [x] Instance stopped before resizing  
- [x] Instance type changed to `t2.nano`  
- [x] Instance restarted successfully  
- [x] Instance state is **Running**  
- [x] Status checks show **2/2 passed**

---

# 🎉 Task Completed Successfully!

The EC2 instance `nautilus-ec2` has been successfully resized from **t2.micro** to **t2.nano** and is now running, ensuring better cost optimization as part of the Nautilus DevOps team’s incremental AWS migration strategy.

---
