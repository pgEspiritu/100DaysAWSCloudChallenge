# 🚀 AWS Task: EC2 + CloudWatch Alarm Setup (Console Method)

## 📌 Objective

Set up monitoring for an EC2 instance with the following:

### 🖥️ EC2 Instance
- Name: `xfusion-ec2`
- AMI: Ubuntu (any Linux)
- Instance type: t2.micro

### 📊 CloudWatch Alarm
- Name: `xfusion-alarm`
- Metric: CPU Utilization
- Statistic: Average
- Threshold: ≥ 90%
- Period: 5 minutes
- Evaluation: 1 datapoint (1 consecutive period)
- Action: Send notification to **SNS topic `xfusion-sns-topic`**

---

# 🧭 Step 1 — Login to AWS Console

1. Open the provided **Console URL**
2. Login using credentials
3. Set region:
```text
us-east-1 (N. Virginia)
```

---

# 🖥️ Step 2 — Launch EC2 Instance

## Navigate:
```text
EC2 → Instances → Launch Instance
```

### Configure:

| Setting | Value |
|---|---|
| Name | xfusion-ec2 |
| AMI | Ubuntu Server |
| Instance Type | t2.micro |
| Key Pair | Optional (Proceed without if allowed) |

---

## Network Settings

- Click **Edit**
- **VPC:** Select default VPC
- **Subnet:** Choose any availability zone
- **🛡️ Auto-assign public IP:** Enable
- **🔒 Firewall (security groups):** 
  - Select **Create security group**
  - **Security group name:** `xfusion-ec2-sg`
  - **Description:** `Security group for xfusion-ec2`
  - **Inbound rules:** Add SSH (port 22) from My IP or 0.0.0.0/0

---

Click:
```text
Launch Instance
```

---

## ✅ Verify Instance

Go to:
```text
EC2 → Instances
```

Ensure:

- State: **Running**
- Status Checks: **2/2 passed**

---

# 📊 Step 3 — Create CloudWatch Alarm

## Navigate:
```text
CloudWatch → Alarms → Create Alarm
```

---

## Step 3.1 — Select Metric

1. Click:
```text
Select metric
```

2. Navigate:
```text
EC2 → Per-Instance Metrics
```

3. Select:
```text
CPUUtilization (for xfusion-ec2)
```

Click:
```text
Select metric
```

---

## Step 3.2 — Configure Metric

| Setting | Value |
|---|---|
| Statistic | Average |
| Period | 5 minutes |

---

## Step 3.3 — Set Threshold

| Setting | Value |
|---|---|
| Threshold type | Static |
| Condition | Greater/Equal |
| Value | 90 |

This means:
```text
CPU ≥ 90% for 5 minutes
```

---

## Step 3.4 — Configure Alarm Actions

1. Under **Alarm state trigger**:
   - Select: **In alarm**

2. Choose SNS topic:
```text
xfusion-sns-topic
```

---

## Step 3.5 — Configure Alarm Name

| Field | Value |
|---|---|
| Alarm name | xfusion-alarm |

Click:
```text
Create alarm
```

---

# 🩺 Step 4 — Verify Alarm

Go to:
```text
CloudWatch → Alarms
```

Check:

- Alarm name: `xfusion-alarm`
- State: **OK** (initially)
- Metric: CPUUtilization

---

# ✅ Final Architecture
```text
EC2 Instance (xfusion-ec2)
│
│ CPU Utilization Metric
▼
CloudWatch Alarm (xfusion-alarm)
│
│ ≥ 90% for 5 min
▼
SNS Topic (xfusion-sns-topic)
│
▼
Notification Sent
```

---

# ✔️ Verification Checklist

| Requirement | Status |
|---|---|
| EC2 instance created | ✅ |
| Name xfusion-ec2 | ✅ |
| Ubuntu AMI used | ✅ |
| Alarm created | ✅ |
| Name xfusion-alarm | ✅ |
| Metric CPU Utilization | ✅ |
| Threshold ≥ 90% | ✅ |
| Period 5 minutes | ✅ |
| SNS topic attached | ✅ |
| Region us-east-1 | ✅ |

---

# 💡 Key Concept

## CloudWatch Alarm Logic
```text
IF CPU ≥ 90% for 1 datapoint (5 mins)
THEN trigger alarm → send SNS notification
```

---

## 🎉 Task Completed Successfully

Your EC2 instance is now actively monitored, and alerts will be sent automatically when CPU usage exceeds the defined threshold.
