# 🚀 AWS Task: EC2 + CloudWatch Alarm Setup (Console Method)

## 📌 Objective

Set up monitoring for an EC2 instance with the following:

### 🖥️ EC2 Instance
- Name: `xfusion-ec2`
- AMI: Ubuntu (any Linux)
- Instance type: t2.micro

### 📊 CloudWatch Alarm
- Name: `xfusion-alarm`
- Metric: CPU Utilization
- Statistic: Average
- Threshold: ≥ 90%
- Period: 5 minutes
- Evaluation: 1 datapoint (1 consecutive period)
- Action: Send notification to **SNS topic `xfusion-sns-topic`**

---

# 🚀 Steps to Create EC2 Instance & CloudWatch Alarm on AWS

## 📋 Prerequisites
- ✅ Access to AWS Console with provided credentials
- 🌎 Region set to `us-east-1`
- 📢 SNS topic named `xfusion-sns-topic` already created

---

## 🔐 Step 1: Login to AWS Console

1. 🌐 Navigate to: `https://252520751240.signin.aws.amazon.com/console?region=us-east-1`
2. 👤 Login with credentials:
   - **Username:** `kk_labs_user_369138`
   - **🔑 Password:** `3wL1XA6mgKn8`

---

## 🖥️ Step 2: Launch EC2 Instance (xfusion-ec2)

### 2.1 Navigate to EC2 Dashboard
1. 🎯 From AWS Console, search for **EC2** in the top search bar
2. Click on **EC2** to open the dashboard

### 2.2 Launch Instance
1. ✅ Click **Launch Instance** button
2. ⚙️ Configure the instance:

#### 📝 **Name and tags:**
- **🏷️ Name:** `xfusion-ec2`

#### 🖼️ **Application and OS Images (Amazon Machine Image - AMI):**
- Choose **Ubuntu** (e.g., Ubuntu Server 22.04 LTS or 24.04 LTS)
- **Architecture:** 64-bit (x86)

#### 🔑 **Key pair (login):**
- Select **Proceed without a key pair** (for lab purposes)
- ⚠️ *Note: Not recommended for production*

#### 🌐 **Network settings:**
- Click **Edit**
- **VPC:** Select default VPC
- **Subnet:** Choose any availability zone
- **🛡️ Auto-assign public IP:** Enable
- **🔒 Firewall (security groups):** 
  - Select **Create security group**
  - **Security group name:** `xfusion-ec2-sg`
  - **Description:** `Security group for xfusion-ec2`
  - **Inbound rules:** Add SSH (port 22) from My IP or 0.0.0.0/0

#### 💾 **Configure storage:**
- **Root volume:** 20 GB gp2 or gp3 (default is fine)

#### 📊 **Advanced details (optional):**
- Keep defaults

### 2.3 Launch Instance
1. 📝 Review all settings
2. ✅ Click **Launch instance**
3. ⏳ Wait for instance to show **Running** state

---

## 📢 Step 3: Create CloudWatch Alarm (xfusion-alarm)

### 3.1 Navigate to CloudWatch
1. 🎯 From AWS Console, search for **CloudWatch**
2. Click on **CloudWatch** to open the dashboard

### 3.2 Create Alarm
1. 📊 In left sidebar, click **Alarms** → **All alarms**
2. ✅ Click **Create alarm** button

### 3.3 Select Metric
1. 🔘 Click **Select metric**
2. 📁 Navigate through:
   - **EC2** → **Per-Instance Metrics**
3. 🔍 Search for instance with `xfusion-ec2` (or find by InstanceId)
4. ✅ Check the box for **CPUUtilization** metric
5. ✅ Click **Select metric**

### 3.4 Configure Alarm Conditions
1. ⚙️ **Specify metric and conditions:**
   - **Statistic:** `Average`
   - **Period:** `5 minutes`
   
2. 📊 **Conditions:**
   - **Threshold type:** Static
   - **Whenever CPUUtilization is:** `Greater/Equal than threshold`
   - **Define the alarm condition:** `90` percent

3. 📈 **Additional configuration:**
   - **Datapoints to alarm:** `1 out of 1` (for 1 consecutive 5-minute period)

4. ✅ Click **Next**

### 3.5 Configure Actions
1. 🔔 **Alarm state trigger:**
   - Select **In alarm**
   
2. 📧 **Send notification to the following SNS topic:**
   - Select **Select an existing SNS topic**
   - **Send a notification to:** Choose `xfusion-sns-topic`
   - *💡 If not showing, refresh or ensure SNS topic exists*

3. ✅ Click **Next**

### 3.6 Add Name and Description
1. 🏷️ **Alarm name:** `xfusion-alarm`
2. 📝 **Alarm description:** `Alarm when CPU utilization exceeds 90% for 1 consecutive 5-minute period`
3. ✅ Click **Next**

### 3.7 Preview and Create
1. 👁️ Review all alarm configuration
2. ✅ Click **Create alarm**

---

## ✅ Step 4: Verify Configuration

### 4.1 Verify EC2 Instance
```bash
# 🖥️ Check instance status
aws ec2 describe-instances --filters "Name=tag:Name,Values=xfusion-ec2" --region us-east-1

---

## 🎉 Task Completed Successfully

Your EC2 instance is now actively monitored, and alerts will be sent automatically when CPU usage exceeds the defined threshold.
