# ✅ AWS Application Load Balancer Setup

## 📌 Objective

Set up an **Application Load Balancer (ALB)** in front of an existing EC2 instance running Nginx.

### Requirements

- ALB Name: **xfusion-alb**
- Target Group: **xfusion-tg**
- Security Group: **xfusion-sg**
- Open **HTTP (Port 80)** publicly
- Route traffic:
```text
ALB :80 → xfusion-ec2 :80
```
- Region: **us-east-1**
- Use **AWS Management Console**

---

# 🧭 Step 1 — Login to AWS Console

1. Open provided **Console URL**
2. Login using credentials
3. Set region (top-right):
```text
us-east-1 (N. Virginia)
```

---

# 🔐 Step 2 — Create Security Group (xfusion-sg)

## Navigate:
```text
EC2 → Security Groups → Create security group
```

### Configure:

| Setting | Value |
|---|---|
| Security group name | xfusion-sg |
| Description | Allow HTTP access to ALB |
| VPC | Default VPC |

### Inbound Rule

| Type | Protocol | Port | Source |
|---|---|---|---|
| HTTP | TCP | 80 | 0.0.0.0/0 |

✅ Click **Create security group**

---

# 🎯 Step 3 — Create Target Group (xfusion-tg)

## Navigate:
```text
EC2 → Target Groups → Create target group
```

### Basic Configuration

| Setting | Value |
|---|---|
| Target type | Instances |
| Target group name | xfusion-tg |
| Protocol | HTTP |
| Port | 80 |
| VPC | Default VPC |

Click **Next**

---

## Register Targets

1. Select instance:
```text
xfusion-ec2
```
2. Click **Include as pending below**
3. Click **Create target group**

---

# ⚖️ Step 4 — Create Application Load Balancer

## Navigate:
```text
EC2 → Load Balancers → Create Load Balancer
```

Select:
```text
Application Load Balancer
```

---

## Basic Configuration

| Setting | Value |
|---|---|
| Name | xfusion-alb |
| Scheme | Internet-facing |
| IP type | IPv4 |

---

## Network Mapping

- Select **Default VPC**
- Select at least **2 Availability Zones**
  - Example:
    - us-east-1a
    - us-east-1b

---

## Security Groups

Select:
```text
xfusion-sg
```

---

## Listeners and Routing

| Setting | Value |
|---|---|
| Protocol | HTTP |
| Port | 80 |
| Forward to | xfusion-tg |

Click:
```text
Create Load Balancer
```


⏳ Wait until ALB state becomes **Active**

---

# 🔓 Step 5 — Update EC2 Security Group (IMPORTANT)

The EC2 instance must allow traffic from the ALB.

## Navigate:
```text
EC2 → Instances → xfusion-ec2
```

Open attached **Security Group**.

### Edit Inbound Rules

Add rule:

| Type | Protocol | Port | Source |
|---|---|---|---|
| HTTP | TCP | 80 | xfusion-sg |

✅ This allows only ALB traffic.

Save rules.

---

# 🩺 Step 6 — Verify Target Health

Navigate:

Open attached **Security Group**.

### Edit Inbound Rules

Add rule:

| Type | Protocol | Port | Source |
|---|---|---|---|
| HTTP | TCP | 80 | xfusion-sg |

✅ This allows only ALB traffic.

Save rules.

---

# 🩺 Step 6 — Verify Target Health

Navigate:
```text
EC2 → Target Groups → xfusion-tg → Targets
```

Wait until:
```text
Health Status = healthy
```

(Health checks may take 1–2 minutes.

---

# 🌐 Step 7 — Test Load Balancer

1. Go to:
```text
EC2 → Load Balancers
```

2. Select:
```text
xfusion-alb
```

3. Copy **DNS Name**

Example:
```text
http://xfusion-alb-123456.us-east-1.elb.amazonaws.com
```

4. Open in browser.

✅ Expected Result:
```text
Nginx default page loads
```

---

# ✅ Final Architecture
```text
Internet
│
▼
Application Load Balancer (xfusion-alb)
│ Port 80
▼
Target Group (xfusion-tg)
│
▼
EC2 Instance (xfusion-ec2 : Nginx)
```

---

# ✔️ Verification Checklist

| Requirement | Status |
|---|---|
| ALB created | ✅ |
| Name xfusion-alb | ✅ |
| Target group created | ✅ |
| Name xfusion-tg | ✅ |
| Security group xfusion-sg | ✅ |
| Port 80 public access | ✅ |
| SG attached to ALB | ✅ |
| Traffic routed to EC2 | ✅ |
| EC2 allows ALB traffic | ✅ |
| Target healthy | ✅ |

---

## 🎉 Task Completed Successfully
Application Load Balancer is now routing traffic to the Nginx EC2 instance.
  
