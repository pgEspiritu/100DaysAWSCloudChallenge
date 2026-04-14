# 🚀 AWS Task: Create Public VPC + Subnet + EC2 (Console Method)

## 📌 Objective

Set up a **public VPC infrastructure** with:

| Resource | Name |
|---------|------|
| VPC | `devops-pub-vpc` |
| Subnet | `devops-pub-subnet` |
| EC2 Instance | `devops-pub-ec2` |
| Instance Type | `t2.micro` |
| Access | SSH (Port 22 open to internet) |
| Region | `us-east-1` |

---

# 🧭 Step 1 — Login to AWS Console

1. Open the provided **Console URL**
2. Login using credentials
3. Set region:
```text
us-east-1 (N. Virginia)
```

---

# 🌐 Step 2 — Create VPC

## Navigate:
```text
VPC → Your VPCs → Create VPC
```

![Day 27.1](images/Day-027.1.png)

### Configure:

| Setting | Value |
|---|---|
| Name | devops-pub-vpc |
| IPv4 CIDR | 10.0.0.0/16 |

![Day 27.2](images/Day-027.2.png)

Click:
```text
Create VPC
```

![Day 27.3](images/Day-027.3.png)

---

# 🌍 Step 3 — Create Public Subnet

## Navigate:
```text
VPC → Subnets → Create subnet
```

![Day 27.4](images/Day-027.4.png)

### Configure:

| Setting | Value |
|---|---|
| VPC | devops-pub-vpc |
| Subnet name | devops-pub-subnet |
| AZ | us-east-1a (or any) |
| CIDR | 10.0.1.0/24 |

Click:
```text
Create subnet
```

![Day 27.5](images/Day-027.5.png)
![Day 27.6](images/Day-027.6.png)

---

# 🌐 Step 4 — Enable Auto Public IP

1. Select subnet:
```text
devops-pub-subnet
```

2. Click:
```text
Actions → Edit subnet settings
```

![Day 27.7](images/Day-027.7.png)

3. Enable:
```text
✔ Auto-assign public IPv4 address
```

Save.

![Day 27.8](images/Day-027.8.png)

---

# 🌍 Step 5 — Create Internet Gateway

## Navigate:
```text
VPC → Internet Gateways → Create
```

![Day 27.9](images/Day-027.9.png)

### Configure:

| Name | devops-igw |

Click:
```text
Create Internet Gateway
```

![Day 27.10](images/Day-027.10.png)

---

## Attach to VPC

1. Select IGW
2. Click:
```text
Actions → Attach to VPC
```

![Day 27.11](images/Day-027.11.png)

3. Choose:
```text
devops-pub-vpc
```

![Day 27.12](images/Day-027.12.png)

---

# 🛣️ Step 6 — Configure Route Table

## Navigate:
```text
VPC → Route Tables
```

1. Find route table linked to your VPC
2. Click → Edit routes

![Day 27.13](images/Day-027.13.png)

Add:

| Destination | Target |
|------------|--------|
| 0.0.0.0/0 | Internet Gateway |

Save.

![Day 27.14](images/Day-027.14.png)

---

## Associate Subnet

1. Go to **Subnet associations**
2. Click:
```text
Edit associations
```

![Day 27.15](images/Day-027.15.png)

3. Select:
```text
devops-pub-subnet
```

save

![Day 27.16](images/Day-027.16.png)

---

# 🔐 Step 7 — Create Security Group

## Navigate:
```text
EC2 → Security Groups → Create
```

![Day 27.17](images/Day-027.17.png)

### Configure:

| Setting | Value |
|---|---|
| Name | devops-pub-sg |
| VPC | devops-pub-vpc |

### Inbound Rule

| Type | Port | Source |
|---|---|---|
| SSH | 22 | 0.0.0.0/0 |

![Day 27.18](images/Day-027.18.png)

Click:
```text
Create security group
```

![Day 27.19](images/Day-027.19.png)

---

# 🖥️ Step 8 — Launch EC2 Instance

## Navigate:
```text
EC2 → Launch Instance
```

![Day 27.20](images/Day-027.20.png)

---

## Configure Instance

| Setting | Value |
|---|---|
| Name | devops-pub-ec2 |
| AMI | Ubuntu (or Amazon Linux) |
| Instance Type | t2.micro |

![Day 27.21](images/Day-027.21.png)
![Day 27.22](images/Day-027.22.png)

---

## Network Settings

| Setting | Value |
|---|---|
| VPC | devops-pub-vpc |
| Subnet | devops-pub-subnet |
| Auto-assign Public IP | Enabled |
| Security Group | devops-pub-sg |

![Day 27.23](images/Day-027.23.png)

---

Click:
```text
Launch Instance
```

---

# ✅ Step 9 — Verify Instance

Go to:
```text
EC2 → Instances
```

Check:

| Item | Expected |
|------|---------|
| Name | devops-pub-ec2 |
| State | Running |
| Public IP | Present |
| SSH | Accessible |

![Day 27.24](images/Day-027.24.png)

---

# 🏁 Final Architecture
```text
Internet
   │
   ▼
Internet Gateway
   │
   ▼
Public Subnet (devops-pub-subnet)
   │
   ▼
EC2 Instance (devops-pub-ec2)
   │
   └── SSH (Port 22 open)
```

---

# ✔️ Verification Checklist

| Requirement                   | Status |
| ----------------------------- | ------ |
| VPC created                   | ✅      |
| Subnet created                | ✅      |
| Public IP auto-assign enabled | ✅      |
| Internet Gateway attached     | ✅      |
| Route table configured        | ✅      |
| Security group allows SSH     | ✅      |
| EC2 instance launched         | ✅      |
| Instance accessible via SSH   | ✅      |
| Region us-east-1              | ✅      |
