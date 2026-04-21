# 🚀 AWS Task: Enable Internet Access via NAT Instance (Console + CLI)

## 📌 Objective

Enable outbound internet access for a **private EC2 instance** using a **NAT Instance** (cost-effective alternative to NAT Gateway).

---

## 🧩 Existing Resources

| Resource | Name |
|---------|------|
| VPC | `nautilus-priv-vpc` |
| Private Subnet | `nautilus-priv-subnet` |
| Private EC2 | `nautilus-priv-ec2` |
| S3 Bucket | `nnautilus-nat-26868` |

---

## 🎯 Tasks

1. Create **Public Subnet** → `nautilus-pub-subnet`
2. Launch **NAT Instance** → `nautilus-nat-instance`
3. Configure NAT (iptables + IP forwarding)
4. Update **Route Tables**
5. Verify upload to S3 (`nautilus-test.txt`)

---

# 🧭 PART 1 — Create Public Subnet

## Navigate:
```text
VPC → Subnets → Create subnet
```

### Configure:

| Setting | Value |
|---|---|
| VPC | nautilus-priv-vpc |
| Subnet Name | nautilus-pub-subnet |
| AZ | us-east-1a |
| CIDR | 10.0.2.0/24 *(or next available range)* |

Click:
```text
Create subnet
```

---

## ✅ Enable Auto Public IP
```text
Select subnet → Actions → Edit subnet settings
```

✔ Enable:
```text
Auto-assign public IPv4
```

---

# 🌐 PART 2 — Internet Gateway Setup

## Create IGW
```text
VPC → Internet Gateways → Create
```

| Name | nautilus-igw |

Attach to:
```text
nautilus-priv-vpc
```

---

# 🛣️ PART 3 — Configure Public Route Table

1. Create or edit route table for public subnet

### Add Route:

| Destination | Target |
|------------|--------|
| 0.0.0.0/0 | Internet Gateway |

---

### Associate with:
```text
nautilus-pub-subnet
```

---

# 🔐 PART 4 — Create NAT Security Group

## Navigate:
```text
EC2 → Security Groups → Create
```

### Configure:

| Setting | Value |
|---|---|
| Name | nautilus-nat-sg |
| VPC | nautilus-priv-vpc |

---

### Inbound Rules:

| Type | Port | Source |
|---|---|---|
| SSH | 22 | 0.0.0.0/0 |
| All Traffic | All | nautilus-priv-subnet CIDR |

---

### Outbound:
```text
Allow All (default)
```

---

# 🖥️ PART 5 — Launch NAT Instance

## Navigate:
```text
EC2 → Launch Instance
```

---

### Configure:

| Setting | Value |
|---|---|
| Name | nautilus-nat-instance |
| AMI | Amazon Linux 2023 |
| Instance Type | t2.micro |
| Subnet | nautilus-pub-subnet |
| Auto Public IP | Enabled |
| Security Group | nautilus-nat-sg |

---

Click:
```text
Launch Instance
```

---

# ⚙️ PART 6 — Configure NAT Instance

## Connect to instance (SSH)

```bash
ssh ec2-user@<NAT-PUBLIC-IP>
```

---

Issue Found: Can't Connect, need to enable public and private keys

### 🔑 STEP 1 — Generate SSH Key (on aws-client)
```bash
ssh-keygen -t rsa -b 2048 -f /root/.ssh/id_rsa -N ""
```

verify:
```bash
ls /root/.ssh/
```

expected:
```text
id_rsa
id_rsa.pub
```

### 📋 STEP 2 — Copy Public Key
```bash
cat /root/.ssh/id_rsa.pub
```
👉 Copy the entire output

### 🌐 STEP 3 — Access EC2 via Console (IMPORTANT)

You cannot SSH yet, so:
- Go to AWS Console
- EC2 → Instances → select your instance
- Click:
```text
Connect → EC2 Instance Connect
```

### 🔧 STEP 4 — Add Your Public Key to EC2

Inside EC2 terminal:
```bash
mkdir -p /home/ec2-user/.ssh
chmod 700 /home/ec2-user/.ssh
```

Now edit:
```bash
nano /home/ec2-user/.ssh/authorized_keys
```
👉 Paste your public key

Save and exit.

### 🔐 STEP 5 — Fix Permissions
```bash
chmod 600 /home/ec2-user/.ssh/authorized_keys
chown -R ec2-user:ec2-user /home/ec2-user/.ssh
```

### 🚀 STEP 6 — SSH Again (from aws-client)
```bash
ssh -i /root/.ssh/id_rsa ec2-user@54.226.240.19
```

### ✅ EXPECTED RESULT
```bash
[ec2-user@ip-...]$
```

🎉 You are now connected

---

## Resume: ⚙️ PART 6 — Configure NAT Instance

## Install iptables
```bash
sudo yum install -y iptables-services
```

## Enable IP Forwarding
```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Make persistent:
```bash
echo "net.ipv4.ip_forward = 1" | sudo tee -a /etc/sysctl.conf
```

## Configure NAT (Masquerading)
```bash
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## Save Rules
```bash
sudo service iptables save
sudo systemctl enable iptables
sudo systemctl start iptables
```

---

# ⚠️ IMPORTANT — Disable Source/Destination Check
In AWS Console:
```text
EC2 → nautilus-nat-instance
```

Actions:
```text
Networking → Change source/destination check → Disable
```

---

# 🛣️ PART 7 — Update Private Route Table
Navigate:
```text
VPC → Route Tables → Private subnet route table
```

Add Route:
| Destination | Target       |
| ----------- | ------------ |
| 0.0.0.0/0   | NAT Instance |

---

# 🧪 PART 8 — Verify Internet Access

Wait 1–2 minutes for cron job.

Check S3 Bucket
```bash
aws s3 ls s3://nautilus-nat-26868
```

---

## Issue: Can't Connect to S3

Steps to Fix:

### 🔐 STEP 1 — Create IAM Role (Console)

**Go to:**
```text
IAM → Roles → Create Role
```

**Configure:**
| Setting        | Value       |
| -------------- | ----------- |
| Trusted Entity | AWS Service |
| Use Case       | EC2         |

**Attach Policy**
Choose:
```text
AmazonS3FullAccess
```
👉 (or at least S3 write access)

Role Name:
```text
nautilus-ec2-role
```

Click:
```text
create role
```

### 🔗 STEP 2 — Attach Role to EC2 Instance

Go to:
```text
EC2 → Instances → datacenter-priv-ec2
```

Action:
```text
Security → Modify IAM Role
```

Select:
```text
datacenter-ec2-role
```

Save.

### ⏳ STEP 3 — Wait ~30 seconds

IAM role propagation takes a bit.

### 🧪 STEP 4 — Test Credentials

Inside EC2:
```text
aws sts get-caller-identity
```

Expected Output:
```json
{
  "Account": "...",
  "Arn": "arn:aws:iam::...:role/datacenter-ec2-role",
  "UserId": "..."
}
```

---

## Resume: Check S3 Bucket

```bash
aws s3 ls s3://nautilus-nat-26868
```

Output:
**No nautilus-test.txt File**

Fix by: Upload manually

### 🧪 STEP 1 — Create the Test File (inside private EC2)

```bash
echo "NAT instance test successful" > nautilus-test.txt
```

### 🚀 STEP 2 — Upload to S3 Manually

```bash
aws s3 cp nautilus-test.txt s3://nautilus-nat-26868/
```

### ✅ Expected Output

```text
upload: ./nautilus-test.txt to s3://nautilus-nat-26868/nautilus-test.txt
```

### Verify Upload

```bash
aws s3 ls s3://nautilus-nat-26868
```

### ✅ Expected Output
```text
nautilus-test.txt
```

✔ This confirms:
- Private EC2 → NAT Instance → Internet → S3 ✅

---

# 🏁 Final Architecture

```text
Private EC2 (nautilus-priv-ec2)
        │
        ▼
Private Subnet
        │
        ▼
NAT Instance (nautilus-nat-instance)
        │
        ▼
Internet Gateway
        │
        ▼
S3 Bucket (nautilus-nat-21059)
```

---

# ✔️ Verification Checklist

| Requirement                | Status |
| -------------------------- | ------ |
| Public subnet created      | ✅      |
| NAT instance launched      | ✅      |
| iptables configured        | ✅      |
| IP forwarding enabled      | ✅      |
| Source/dest check disabled | ✅      |
| Route tables updated       | ✅      |
| Private EC2 has internet   | ✅      |
| File uploaded to S3        | ✅      |
