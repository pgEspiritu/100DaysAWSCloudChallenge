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

## 🌍 Step 1: Log in to AWS Console

1. Open the **Console URL** provided above
2. Enter the **username** and **password**
3. Successfully sign in to the AWS Management Console

---

## 🌐 Step 2: Verify the AWS Region

1. Look at the **top-right corner** of the console
2. Ensure the selected region is:

```text
N. Virginia (us-east-1)
```

> ⚠️ If not, switch to **us-east-1**, as required.

---

### Step 3️⃣: Navigate to EC2 Service
1. From the AWS Console homepage, search for **EC2**.
2. Click **EC2** to open the EC2 Dashboard.

---

### Step 4️⃣: Open Key Pairs Section
1. In the EC2 left-hand navigation pane, scroll down to **Network & Security**.
2. Click on **Key Pairs**.

---

### Step 5️⃣: Create a New Key Pair
1. Click the **Create key pair** button.
2. Fill in the following details:

| Field | Value |
|-----|------|
| **Name** | `xfusion-kp` |
| **Key pair type** | `RSA` |
| **Private key file format** | `.pem` (default) |

---

### Step 6️⃣: Create and Download Key
1. Click **Create key pair**.
2. The private key file (`xfusion-kp.pem`) will be downloaded automatically.
3. Store the file in a **secure location**.

> ⚠️ **Important:** AWS does **not** allow re-downloading private keys.

---

### Step 7️⃣: Verify Key Pair Creation
1. Confirm that `xfusion-kp` appears in the **Key Pairs** list.
2. Ensure:
   - Status: **Available**
   - Type: **RSA**

---

## ✅ Final Validation Checklist

- [x] Key pair name is `xfusion-kp`  
- [x] Key pair type is **RSA**  
- [x] Created in **us-east-1** region  
- [x] Private key downloaded successfully  

---

## 🎉 Task Completed Successfully!

The EC2 key pair required for the incremental AWS migration has been created successfully using the **AWS Management Console**.  
This key pair can now be used for secure access to EC2 instances during future migration phases.

---


