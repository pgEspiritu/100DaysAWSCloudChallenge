# 🚀 AWS Task: Create AMI from EC2 Instance (Console)

## 🧩 Scenario

The **Nautilus DevOps Team** is migrating parts of their infrastructure to AWS in incremental steps.  
To support backup, scaling, and reproducibility, they need to create an **Amazon Machine Image (AMI)** from an existing EC2 instance.

---

## 🎯 Objective

Create an **AMI** from the existing EC2 instance with the following details:

| Resource | Name |
|--------|------|
| EC2 Instance | `xfusion-ec2` |
| AMI Name | `xfusion-ec2-ami` |
| Region | `us-east-1` |

The AMI must reach the **Available** state before the task is considered complete.

---

## 🧭 Step 1 — Login to AWS Console

1. Open the provided **Console URL**.
2. Sign in using the provided credentials.
3. Verify the region is set to:
```text
us-east-1 (N. Virginia)
```

You can check or change the region in the **top-right corner** of the AWS Console.

---

## 🖥️ Step 2 — Navigate to EC2 Instances

1. Open the **EC2 Dashboard**.
2. Click:
```text
Instances
```

3. Locate the instance:
```text
xfusion-ec2
```


4. Verify that the instance state is:
```text
Running
```

---

## 📸 Step 3 — Create AMI

1. Select the instance **xfusion-ec2**.
2. Click **Actions**.
3. Navigate to:
```text
Image and templates → Create image
```

4. Configure the image details:

| Setting | Value |
|-------|------|
| Image name | `xfusion-ec2-ami` |
| Image description | Optional |

5. Leave other settings as default.

6. Click:
```text
Create image
```

---

## 🔍 Step 4 — Monitor AMI Creation

1. After creating the image, go to:
```text
EC2 Dashboard → Images → AMIs
```

2. Search for:
```text
xfusion-ec2-ami
```

3. Wait until the **AMI state** changes from:
```text
Pending → Available
```

---

## ✅ Verification Checklist

- [x] Logged into AWS Console
- [x] Region set to `us-east-1`
- [x] Located instance `xfusion-ec2`
- [x] Created AMI named `xfusion-ec2-ami`
- [x] AMI state shows **Available**

---

## 🏁 Result

The **AMI `xfusion-ec2-ami`** has been successfully created from the EC2 instance **xfusion-ec2** and is now in the **Available** state.

---

## 💡 Key Concepts

- **Amazon Machine Image (AMI)** for creating EC2 templates
- Backup and replication of EC2 instances
- Infrastructure reproducibility in AWS
- EC2 image lifecycle management

---

## 📸 Suggested Screenshots (for GitHub Portfolio)

- EC2 Instances page showing `xfusion-ec2`
- Create Image configuration page
- AMI creation progress
- AMI status showing **Available**
