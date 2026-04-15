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

# 🧭 PART 1 — Create VPC Peering Connection

## Navigate:
```text
VPC → Peering Connections → Create Peering Connection
```

### Configure:

| Setting | Value |
|---|---|
| Name | devops-vpc-peering |
| VPC (Requester) | Default VPC |
| VPC (Accepter) | devops-private-vpc |

Click:
```text
Create Peering Connection
```

---

## Accept Peering

1. Select peering connection
2. Click:
```text
Actions → Accept Request
```

✅ Status should be:
```text
Active
```

---

# 🛣️ PART 2 — Update Route Tables

## 📍 2.1 Public VPC Route Table

Navigate:
```text
VPC → Route Tables → Default VPC Route Table
```

Edit routes:

| Destination | Target |
|------------|--------|
| 10.1.0.0/16 | Peering Connection |

Save.

---

## 📍 2.2 Private VPC Route Table

Navigate:
```text
Route table for devops-private-vpc
```

Edit routes:

| Destination | Target |
|------------|--------|
| Default VPC CIDR (e.g., 172.31.0.0/16) | Peering Connection |

Save.

---

# 🔐 PART 3 — Update Security Groups

## 📍 3.1 Private EC2 Security Group

Navigate:
```text
EC2 → devops-private-ec2 → Security Group
```


### Add Inbound Rules:

| Type | Port | Source |
|---|---|---|
| SSH | 22 | Default VPC CIDR |
| ICMP | All | Default VPC CIDR |

---

## 📍 3.2 Public EC2 Security Group (Optional)

Allow SSH from aws-client if needed:

| Type | Port | Source |
|---|---|---|
| SSH | 22 | Your IP / 0.0.0.0/0 |

---

# 🔑 PART 4 — Setup SSH Access (aws-client → Public EC2)

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

# 🏁 Final Architecture

```text
aws-client
   │
   ▼
Public EC2 (devops-public-ec2)
   │
   │ VPC Peering
   ▼
Private EC2 (devops-private-ec2)
```

---

# ✔️ Verification Checklist

| Requirement                | Status |
| -------------------------- | ------ |
| Peering created            | ✅      |
| Peering active             | ✅      |
| Routes updated (both VPCs) | ✅      |
| Security groups updated    | ✅      |
| SSH to public EC2 works    | ✅      |
| Ping to private EC2 works  | ✅      |

---

# 💡 Key Concepts
VPC Peering
- Enables private communication between VPC
- Uses private IPs
- Requires:
  - Route table updates
  - Security group rules
 
## Traffic Flow
```text
Public EC2 → Route Table → Peering → Private EC2
```
