# 🚀 AWS DevOps Task – Create an EC2 Key Pair (Step-by-Step Solution)

The **Nautilus DevOps team** is performing a **phased migration** to the cloud to reduce risk and improve control over the process. As part of this incremental strategy, they are creating foundational AWS resources in small, manageable steps.

In this task, we will **create an EC2 key pair** in **:contentReference[oaicite:0]{index=0} (AWS)** using the provided credentials.

---

## 🧩 Task Requirements

| Requirement | Value |
|------------|------|
| **Key Pair Name** | `xfusion-kp` |
| **Key Pair Type** | `rsa` |
| **AWS Region** | `us-east-1` |
| **Method** | AWS CLI (from aws-client host) |

---

## 🔐 Provided AWS Credentials

> ⚠️ **Note:** These credentials are **temporary** and valid only during the given time window.

- **Console URL:** https://915501509755.signin.aws.amazon.com/console?region=us-east-1  
- **Username:** `kk_labs_user_287126`  
- **Password:** `t^k1!7Cm!dYt`  
- **Start Time:** Sun Feb 22 22:50:53 UTC 2026  
- **End Time:** Sun Feb 22 23:50:53 UTC 2026  

You may retrieve credentials directly on the AWS client machine using:

```bash
showcreds
```

---

## 🛠️ Step-by-Step Solution (AWS CLI)
Step 1: Access the AWS Client Host

Log in to the aws-client machine provided in the lab environment.

---

## Step 2: Verify AWS CLI Configuration

Ensure the AWS CLI is authenticated and set to the correct region:

```bash
aws configure
```

Enter the credentials obtained from showcreds, and set:

```bash
Default region name: us-east-1
Default output format: json
```

---

## Step 3: Create the RSA Key Pair

Run the following command to create the key pair:

```bash
aws ec2 create-key-pair \
  --key-name xfusion-kp \
  --key-type rsa \
  --query 'KeyMaterial' \
  --output text > xfusion-kp.pem
```

✅ This command:
- Creates an RSA key pair
- Saves the private key locally as xfusion-kp.pem

---

## Step 4: Secure the Private Key

Restrict file permissions (required for SSH access):

```bash
chmod 400 xfusion-kp.pem
```

---

## Step 5: Verify Key Pair Creation

Confirm that the key pair exists in AWS:

```bash
aws ec2 describe-key-pairs --key-names xfusion-kp
```
Expected result: details of the xfusion-kp key pair.

---

## ✅ Final Outcome
- ✔ Key pair xfusion-kp created successfully
- ✔ Key type: RSA
- ✔ Region: us-east-1
- ✔ Private key stored securely

This key pair can now be used for secure SSH access to EC2 instances as part of the Nautilus team’s phased AWS migration strategy.
