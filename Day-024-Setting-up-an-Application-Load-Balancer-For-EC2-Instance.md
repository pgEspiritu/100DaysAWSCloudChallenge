# 🚀 Steps to Configure Application Load Balancer (ALB) on AWS

## 📋 Prerequisites
- ✅ Access to AWS Console with provided credentials
- 🖥️ EC2 instance named `nautilus-ec2` already running with Nginx on port 80
- 🌎 Region set to `us-east-1`

---

## 🔐 Step 1: Login to AWS Console

1. 🌐 Navigate to: `https://717866278654.signin.aws.amazon.com/console?region=us-east-1`
2. 👤 Login with credentials:
   - **Username:** `kk_labs_user_855470`
   - **🔑 Password:** `8rt^N@0FM1FM`

---

## 🛡️ Step 2: Create Security Group for ALB

1. 🎯 Navigate to **VPC** → **Security Groups** → **Create security group**
2. ⚙️ Configure:
   - **🏷️ Security group name:** `nautilus-sg`
   - **📝 Description:** `Security group for ALB - port 80 public access`
   - **🌐 VPC:** Select default VPC
3. **📥 Inbound rules:**
   - **🔌 Type:** HTTP
   - **📡 Protocol:** TCP
   - **🔢 Port range:** 80
   - **🌍 Source:** 0.0.0.0/0 (Anywhere-IPv4)
4. **📤 Outbound rules:** Keep default (all traffic allowed)
5. ✅ Click **Create security group**

---

## 🎯 Step 3: Create Target Group

1. 🎯 Navigate to **EC2** → **Target Groups** → **Create target group**
2. ⚙️ **Basic configuration:**
   - **🖱️ Choose target type:** Instances
   - **🏷️ Target group name:** `nautilus-tg`
   - **🔌 Protocol:** HTTP
   - **🔢 Port:** 80
   - **🌐 VPC:** Select default VPC
   - **📦 Protocol version:** HTTP1
3. ❤️ **Health checks:**
   - **🔌 Health check protocol:** HTTP
   - **📁 Health check path:** /
   - **⚙️ Advanced health check settings:** Keep defaults
4. ⏩ Click **Next**
5. **📋 Register targets:**
   - ✅ Select the `nautilus-ec2` instance
   - ➕ Click **Include as pending below**
   - ✅ Click **Create target group**

---

## ⚖️ Step 4: Create Application Load Balancer

1. 🎯 Navigate to **EC2** → **Load Balancers** → **Create Load Balancer**
2. 🏗️ Select **Application Load Balancer**
3. ⚙️ **Basic configuration:**
   - **🏷️ Load balancer name:** `nautilus-alb`
   - **🌍 Scheme:** Internet-facing
   - **🔢 IP address type:** IPv4
4. 🌐 **Network mapping:**
   - **VPC:** Select default VPC
   - **📍 Mappings:** Select at least two availability zones with subnets
5. 🛡️ **Security groups:**
   - ❌ Remove default security group
   - ✅ Select `nautilus-sg` (created in Step 2)
6. 🎧 **Listeners and routing:**
   - **🔌 Protocol:** HTTP
   - **🔢 Port:** 80
   - **➡️ Default action:** Forward to `nautilus-tg`
7. ✅ Click **Create load balancer**

---

## 🔧 Step 5: Update EC2 Instance Security Group

1. 🖥️ Navigate to **EC2** → **Instances**
2. ✅ Select `nautilus-ec2` instance
3. 🔒 Click **Security** tab → Click security group link
4. ✏️ **Edit inbound rules:**
   - ➕ Add rule:
     - **🔌 Type:** HTTP
     - **📡 Protocol:** TCP
     - **🔢 Port:** 80
     - **🌐 Source:** 
       - Select **Custom**
       - Enter the security group ID of `nautilus-sg` (e.g., `sg-xxxxxxxxx`)
       - *🔐 This allows traffic only from the ALB security group*
   - 💡 Alternatively, you can allow traffic from the ALB's VPC CIDR block

---

## ✅ Step 6: Verify Configuration

1. ⏳ Wait for ALB provisioning to complete (provisioning state becomes **Active**)
2. 📋 Copy the **DNS name** of `nautilus-alb` (e.g., `nautilus-alb-1234567890.us-east-1.elb.amazonaws.com`)
3. 🧪 Test by accessing the DNS name in a web browser
4. 🎉 You should see the Nginx default page or sample application page

---

## 💻 Verification Commands (Optional)

```bash
# 🧪 Test ALB DNS endpoint
curl http://nautilus-alb-1150587295.us-east-1.elb.amazonaws.com

# 📊 Check target health
aws elbv2 describe-target-health --target-group-arn <target-group-arn> --region us-east-1
