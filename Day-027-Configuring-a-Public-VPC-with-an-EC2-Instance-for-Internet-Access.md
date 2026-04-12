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

### Configure:

| Setting | Value |
|---|---|
| Name | devops-pub-vpc |
| IPv4 CIDR | 10.0.0.0/16 |

Click:
```text
Create VPC
```

---

# 🌍 Step 3 — Create Public Subnet

## Navigate:
```text
VPC → Subnets → Create subnet
```

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

3. Enable:
```text
✔ Auto-assign public IPv4 address
```

Save.

---

# 🌍 Step 5 — Create Internet Gateway

## Navigate:
```text
VPC → Internet Gateways → Create
```

### Configure:

| Name | devops-igw |

Click:
```text
Create Internet Gateway
```

---

## 🛣️ Step 6 — Configure Route Table & Associate Subnet

## Attach to VPC

1. 📋 Select the internet gateway devops-pub-igw
2. ✅ Click Actions → Attach to VPC
3. 🔗 Available VPCs: Select devops-pub-vpc
4. ✅ Click Attach internet gateway

---

## Create Route Table

1. 🗺️ In VPC Dashboard, click Route Tables in left sidebar
2. ✅ Click Create route table
3. 🏷️ Name: devops-pub-rt
4. 🧩 VPC: Select devops-pub-vpc
5. ✅ Click Create route table

---

## Add Route to Internet Gateway
- 📋 Select the route table devops-pub-rt
- 📊 Click Routes tab → Edit routes
- ✅ Click Add route
- 🌐 Destination: 0.0.0.0/0
- 🎯 Target: Select Internet Gateway → devops-pub-igw
- ✅ Click Save changes

## Associate Subnet
- 🔗 Click Subnet associations tab
- ✅ Click Edit subnet associations
- ✅ Select devops-pub-subnet
- ✅ Click Save associations

---

# 🔐 Step 7 — Create Security Group

## Navigate:
```text
EC2 → Security Groups → Create
```

### Configure:

| Setting | Value |
|---|---|
| Name | devops-pub-sg |
| VPC | devops-pub-vpc |

### Inbound Rule

| Type | Port | Source |
|---|---|---|
| SSH | 22 | 0.0.0.0/0 |

Click:
```text
Create security group
```

---

# 🖥️ Step 8 — Launch EC2 Instance

## Navigate:
```text
EC2 → Launch Instance
```

---

## Configure Instance

| Setting | Value |
|---|---|
| Name | devops-pub-ec2 |
| AMI | Ubuntu (or Amazon Linux) |
| Instance Type | t2.micro |

---

## Network Settings

| Setting | Value |
|---|---|
| VPC | devops-pub-vpc |
| Subnet | devops-pub-subnet |
| Auto-assign Public IP | Enabled |
| Security Group | devops-pub-sg |

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

---

# 🔗 Step 10 — Test SSH Access

From terminal:

```bash
ssh ubuntu@<PUBLIC-IP>
```
(or ec2-user depending on AMI)

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
