# 🚀 AWS Task: VPC Peering + EC2 Connectivity (Console + CLI)

## 📌 Objective

Enable communication between:

| VPC Type | Resource |
|----------|---------|
| Public VPC (Default) | `devops-public-ec2` |
| Private VPC | `devops-private-vpc` |
| Private EC2 | `devops-private-ec2` |

### Requirements
- Create **VPC Peering**
- Configure **Route Tables**
- Update **Security Groups**
- Enable **SSH + Ping (ICMP)**
- Verify connectivity from public → private EC2

---

# 🔗 Steps to Configure VPC Peering for Cross-VPC Communication

## 📋 Prerequisites
- ✅ Access to AWS Console with provided credentials
- 🌎 Region set to `us-east-1`
- ✅ Default VPC exists with public EC2 instance: `xfusion-public-ec2`
- ✅ Private VPC exists: `xfusion-private-vpc` (10.1.0.0/16)
- ✅ Private subnet exists: `xfusion-private-subnet` (10.1.1.0/24)
- ✅ Private EC2 instance exists: `xfusion-private-ec2`

---

## 🔐 Step 1: Login to AWS Console

1. 🌐 Navigate to: `https://658733160186.signin.aws.amazon.com/console?region=us-east-1`
2. 👤 Login with credentials:
   - **Username:** `kk_labs_user_971918`
   - **🔑 Password:** `uk^CDxP9Q620`

---

## 🔗 Step 2: Create VPC Peering Connection

### 2.1 Navigate to VPC Dashboard
1. 🎯 From AWS Console, search for **VPC**
2. Click on **VPC** to open the dashboard

### 2.2 Create Peering Connection
1. 📁 In left sidebar, click **Peering Connections**
2. ✅ Click **Create Peering Connection**

#### ⚙️ Configure peering:
- **🏷️ Peering connection name tag:** `xfusion-vpc-peering`
- **🧩 VPC (Requester):** Select the **Default VPC**
  - *Look for VPC with "(default)" in name*
  - *Example CIDR: 172.31.0.0/16 or 172.16.0.0/16*
- **🧩 VPC (Accepter):** Select `xfusion-private-vpc` (10.1.0.0/16)
- **📡 Accepter account:** My account

3. ✅ Click **Create Peering Connection**
4. 📋 Note the **Peering Connection ID** (e.g., `pcx-12345678`)

### 2.3 Accept Peering Connection
1. ✅ Select the peering connection `xfusion-vpc-peering`
2. 🔘 Click **Actions** → **Accept request**
3. ✅ Click **Accept request** in confirmation dialog
4. 🎉 Status should change to `Active`

---

## 🗺️ Step 3: Configure Route Tables

### 3.1 Identify Route Tables

#### Default VPC Route Table:
```bash
# Find default VPC ID
aws ec2 describe-vpcs --filters "Name=isDefault,Values=true" --query "Vpcs[0].VpcId" --output text

# Find default VPC's main route table
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=<default-vpc-id>" "Name=association.main,Values=true"
```

Private VPC Route Table:
```bash
# Find private VPC ID
aws ec2 describe-vpcs --filters "Name=tag:Name,Values=xfusion-private-vpc" --query "Vpcs[0].VpcId" --output text

# Find private subnet's route table
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=<private-vpc-id>" "Name=association.subnet-id,Values=<private-subnet-id>"
```

---

### 3.2 Add Route to Default VPC Route Table

1. 📁 In VPC Dashboard, click Route Tables
2. 🔍 Find the route table associated with Default VPC
   - Look for main route table of default VPC
4. ✅ Select the route table
5. 📊 Click Routes tab → Edit routes
6. ✅ Click Add route
   - 🌐 Destination: 10.1.0.0/16 (private VPC CIDR)
   - 🎯 Target: Select Peering Connection → xfusion-vpc-peering
7. ✅ Click Save changes

---

### 3.3 Add Route to Private VPC Route Table

1. 🔍 Find the route table associated with Private VPC (xfusion-private-vpc)
2. ✅ Select the route table
3. 📊 Click Routes tab → Edit routes
4. ✅ Click Add route
   - 🌐 Destination: `<default-vpc-cidr>` (e.g., 172.31.0.0/16)
   - 🎯 Target: Select Peering Connection → xfusion-vpc-peering
5. ✅ Click Save changes

---

### 3.4 Verify Routes

```bash
# Check routes in default VPC route table
aws ec2 describe-route-tables --route-table-ids <default-rt-id> \
  --query "RouteTables[0].Routes[?DestinationCidrBlock=='10.1.0.0/16']"

# Check routes in private VPC route table
aws ec2 describe-route-tables --route-table-ids <private-rt-id> \
  --query "RouteTables[0].Routes[?DestinationCidrBlock=='<default-vpc-cidr>']"
```

---

## 🔒 Step 4: Configure Security Groups

### 4.1 Update Private EC2 Security Group
1. 🛡️ Go to EC2 → Security Groups
2. 🔍 Find security group attached to xfusion-private-ec2
3. ✅ Select the security group
4. 📊 Click Inbound rules tab → Edit inbound rules
5. ✅ Add rule for ICMP (ping):
   - Type: All ICMP - IPv4
   - Source: `<default-vpc-cidr>`  (e.g., 172.31.0.0/16)
   - Description: Allow ping from default VPC
6. (Optional) Add rule for SSH if needed:
   - Type: SSH
   - Source: `<default-vpc-cidr>` 
7. ✅ Click Save rules

---

### 4.2 Update Public EC2 Security Group (Optional)

If you need to SSH from public instance to private instance:
1. 🔍 Find security group attached to xfusion-public-ec2
2. 📊 Add outbound rule:
   - Type: SSH (port 22)
   - Destination: 10.1.0.0/16 (private VPC CIDR)
3. 📊 Add inbound rule:
   - Type: SSH (port 22)
   - Destination: Anywhere IPV4

---

## 🔑 Step 5: Setup SSH Access (aws-client → Public EC2)

## On aws-client

### Check key:

```bash
ls /root/.ssh/id_rsa.pub
```

If not exists:

```bash
ssh-keygen -t rsa -f /root/.ssh/id_rsa -N ""
```

### Copy Public Key
```bash
cat /root/.ssh/id_rsa.pub
```

### Add to Public EC2
1. Connect via EC2 Instance Connect
2. Edit:
```bash
nano /home/ec2-user/.ssh/authorized_keys
```
Paste key.

Fix permissions:
```bash
chmod 600 ~/.ssh/authorized_keys
```

---

# 🔗 PART 5 — SSH into Public EC2

From aws-client:
```bash
ssh ec2-user@<PUBLIC-EC2-IP>
```

---

# 🧪 PART 6 — Test Connectivity (Public → Private EC2)
Get Private EC2 IP

From AWS Console:
```text
devops-private-ec2 → Private IP
```

### Ping Private EC2

Inside public EC2:
```bash
ping <PRIVATE-IP>
```

✅ Expected Output
```text
64 bytes from <PRIVATE-IP>: icmp_seq=1 ttl=...
```

---

## ✅ Final Verification Checklist

- 🔗 VPC Peering xfusion-vpc-peering created and Active
- 🗺️ Default VPC route table has route to 10.1.0.0/16 via peering
- 🗺️ Private VPC route table has route to default VPC CIDR via peering
- 🛡️ Private EC2 security group allows ICMP from default VPC CIDR
- 🔑 Public key added to xfusion-public-ec2 authorized_keys
- 🖥️ Able to SSH from AWS client to public EC2 instance
- 📡 From public EC2, able to ping private EC2 instance
- ✅ Cross-VPC communication working

---

## Configured Successfully

- 🔗 xfusion-vpc-peering - VPC peering between default and private VPCs
- 🗺️ Route tables - Routes for cross-VPC communication
- 🛡️ Security groups - Allow ICMP from public VPC to private EC2
- 🔑 SSH access - From AWS client to public EC2 instance
- 📡 Connectivity - Public EC2 can ping private EC2 instance

---

## 🌐 Architecture Overview

```text
[AWS Client Host]
       ↓ (SSH)
[Public EC2: xfusion-public-ec2]
       ↓ (ICMP via VPC Peering)
[Private EC2: xfusion-private-ec2]
       ↑
[Default VPC] ←→ [xfusion-vpc-peering] ←→ [xfusion-private-vpc]
```
