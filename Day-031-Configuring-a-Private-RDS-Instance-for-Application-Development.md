# 🚀 AWS Task: Create Private RDS MySQL Instance (Free Tier)

## 📌 Objective

Provision a **private Amazon RDS MySQL database** for development use.

---

## 🧩 Requirements

| Setting | Value |
|--------|------|
| DB Identifier | `devops-rds` |
| Engine | MySQL |
| Version | 8.4.x |
| Instance Class | `db.t3.micro` |
| Template | Free Tier |
| Deployment | Private RDS |
| Storage Autoscaling | Enabled |
| Max Storage Threshold | 50 GB |
| Status | Available |

---

# 🧭 STEP 1 — Open RDS Console

Navigate:
```text
AWS Console → RDS
```

Ensure region:
```text
us-east-1 (N. Virginia)
```


---

# 🗄️ STEP 2 — Create Database

Click:
```text
Create database
```

![Day 31.1](images/Day-031.1.png)

---

## ⚙️ Choose Creation Method

Select:
```text
Standard create (Full configuration)
```

![Day 31.2](images/Day-031.2.png)
![Day 31.3](images/Day-031.3.png)

---

# 🐬 STEP 3 — Engine Selection

| Setting | Value |
|--------|------|
| Engine type | MySQL |
| Version | 8.4.x |

---

# 💰 STEP 4 — Templates

Select:
```text
Free tier
```

![Day 31.4](images/Day-031.4.png)
![Day 31.5](images/Day-031.5.png)

---

# 🧾 STEP 5 — DB Settings

| Setting | Value |
|--------|------|
| DB instance identifier | devops-rds |
| Master username | admin (default or keep provided) |
| Password | Set secure password |

![Day 31.6](images/Day-031.6.png)

---

# 🖥️ STEP 6 — Instance Class

Select:
```text
db.t3.micro
```

![Day 31.7](images/Day-031.7.png)

---

# 🌐 STEP 7 — Connectivity (IMPORTANT)

| Setting | Value |
|--------|------|
| Public access | ❌ No (Private DB) |
| VPC | Default or provided VPC |
| Subnet group | Default |
| Security group | default or create new |

![Day 31.8](images/Day-031.8.png)
![Day 31.9](images/Day-031.9.png)

---

# 💾 STEP 8 — Storage Configuration

Enable:
```text
✔ Storage autoscaling
```

Set:
```text
Maximum threshold = 50 GB
```

![Day 31.10](images/Day-031.10.png)

Leave everything else default.

---

# 🔐 STEP 9 — Additional Settings

Leave defaults unless required.

---

# 🚀 STEP 10 — Create Database

Click:
```text
Create database
```

![Day 31.11](images/Day-031.11.png)

---

# ⏳ STEP 11 — Wait for Availability

Go to:
```text
RDS → Databases → devops-rds
```

Wait until status:
```text
Available
```

![Day 31.12](images/Day-031.12.png)

---

# 🧪 STEP 12 — Verification Checklist

| Requirement | Status |
|------------|--------|
| MySQL 8.4.x | ✅ |
| db.t3.micro | ✅ |
| Private DB | ✅ |
| Free tier template | ✅ |
| Storage autoscaling enabled | ✅ |
| Max 50 GB set | ✅ |
| Status = Available | ✅ |

---

# 🏁 Architecture Summary

``` id="rdsarch1"
Application Layer
        │
        ▼
Private RDS (devops-rds)
        │
   MySQL 8.4.x Engine
```

---

# 💡 Key Notes
Why Private RDS?
- No public internet exposure
- Secure internal DB access
- Best practice for production-like setups
