# 🚀 AWS Task: Attach Elastic Network Interface via AWS Console

## 🧩 Problem Overview

The **Nautilus DevOps Team** is performing incremental migration tasks in AWS to improve operational control, reduce risks, and optimize resource utilization.

An existing EC2 instance needs an additional network interface attached using the **AWS Management Console**.

---

## 🎯 Objective

Attach an existing **Elastic Network Interface (ENI)** to an existing EC2 instance.

---

## 📋 Requirements

| Resource | Name |
|----------|------|
| EC2 Instance | `nautilus-ec2` |
| Network Interface | `nautilus-eni` |
| Region | `us-east-1` |

✅ Ensure instance initialization is completed.  
✅ Ensure network interface status becomes **Attached** before submission.

---

## 🧭 Step 1 — Login to AWS Console

1. Open the provided **Console URL**.
2. Login using the provided credentials.
3. Confirm region is set to:
```text
us-east-1 (N. Virginia)
```

📍 Top-right corner → Region Selector.

---

## 🖥️ Step 2 — Verify EC2 Instance Status

1. Navigate to:
```text
EC2 Dashboard → Instances
```

2. Locate instance:
```text
nautilus-ec2
```

3. Verify:

| Check | Expected Status |
|------|-----------------|
| Instance State | Running |
| Status Check | 2/2 checks passed |

⚠️ If status shows **Initializing**, wait until checks complete.

---

## 🌐 Step 3 — Locate Network Interface

1. From EC2 left navigation panel:
```text
Network & Security → Network Interfaces
```

2. Search for:
```text
nautilus-eni
```

3. Confirm status:
```text
Available
```

---

## 🔗 Step 4 — Attach Network Interface

1. Select **nautilus-eni**
2. Click **Actions**
3. Choose:
```text
Attach
```
4. Configure attachment:

| Setting | Value |
|--------|-------|
| Instance | `nautilus-ec2` |
| Device Index | `1` |

📌 Device index `0` is reserved for the primary interface.

5. Click:
```text
Attach network interface
```

---

## ✅ Step 5 — Verify Attachment

After attaching:

1. Refresh the page.
2. Check ENI details.

Expected values:

| Property | Expected Value |
|----------|---------------|
| Status | `In-use` |
| Attachment Status | `Attached` |
| Instance ID | nautilus-ec2 instance |

---

## ✔️ Validation Checklist

- [x] Logged into AWS Console
- [x] Region set to `us-east-1`
- [x] Instance initialization completed
- [x] Network interface attached
- [x] ENI status shows **In-use**
- [x] Attachment status shows **Attached**

---

## 🏁 Result

The **Elastic Network Interface (`nautilus-eni`)** has been successfully attached to the **EC2 instance (`nautilus-ec2`)** using the AWS Management Console.

---

## 💡 Key Concepts Learned

- Elastic Network Interfaces (ENI)
- Instance initialization checks
- Secondary network interface attachment
- AWS Console resource management

---
