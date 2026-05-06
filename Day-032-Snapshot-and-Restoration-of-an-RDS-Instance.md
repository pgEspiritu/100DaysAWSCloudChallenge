# 🚀 AWS Task: RDS Snapshot & Restore (Console Method)

## 📌 Objective

Safely back up and validate your database by:

1. Creating a snapshot of `devops-rds`
2. Restoring it to a new instance `devops-snapshot-restore`
3. Ensuring the new DB is **Available**

---

## 🧩 Requirements

| Task | Value |
|------|------|
| Source DB | devops-rds |
| Snapshot Name | devops-snapshot |
| Restored DB | devops-snapshot-restore |
| Instance Class | db.t3.micro |
| Region | us-east-1 |

---

# 🧭 STEP 1 — Verify Source DB Status

Navigate:
```text
RDS → Databases → devops-rds
```

✅ Ensure status:
```text
Available
```

---

# 📸 STEP 2 — Create Snapshot

1. Select:
```text
devops-rds
```

2. Click:
```text
Actions → Take snapshot
```

---

### Configure:

| Setting | Value |
|--------|------|
| Snapshot name | devops-snapshot |

Click:
```text
Take snapshot
```

---

## ⏳ Wait for Snapshot

Navigate:
```text
RDS → Snapshots
```

Wait until:
```text
Status = Available
```

---

# ♻️ STEP 3 — Restore Snapshot

1. Select snapshot:
```text
devops-snapshot
```

2. Click:
```text
Actions → Restore snapshot
```

---

# ⚙️ STEP 4 — Configure Restored DB

### Basic Settings

| Setting | Value |
|--------|------|
| DB instance identifier | devops-snapshot-restore |

---

### Instance Configuration

| Setting | Value |
|--------|------|
| DB instance class | db.t3.micro |

---

### Connectivity

| Setting | Value |
|--------|------|
| Public access | No (keep private) |
| VPC | Same as original |
| Security group | Default or same |

---

Leave all other settings as default.

---

Click:
```text
Restore DB instance
```

---

# ⏳ STEP 5 — Wait for Restoration

Navigate:
```text
RDS → Databases → devops-snapshot-restore
```

Wait until:
```text
Status = Available
```

---

# ✅ STEP 6 — Verification Checklist

| Requirement | Status |
|------------|--------|
| Snapshot created | ✅ |
| Snapshot name correct | ✅ |
| Snapshot available | ✅ |
| Restored DB created | ✅ |
| Instance class = db.t3.micro | ✅ |
| DB is private | ✅ |
| Status = Available | ✅ |

---

# 🏁 Architecture Overview

``` id="rdsflow2"
devops-rds (Original DB)
        │
        ▼
Snapshot (devops-snapshot)
        │
        ▼
Restored DB (devops-snapshot-restore)
```

---

## 💡 Key Concepts
Why Snapshot?
- Backup before major changes
- Data recovery
- Clone environments for testing

## Restore Benefits
- Validate backup integrity
- Test changes safely
- No impact on production DB
