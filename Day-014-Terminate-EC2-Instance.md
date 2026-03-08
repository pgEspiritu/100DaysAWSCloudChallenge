# 🚀 AWS Task: Delete EC2 Instance (Console)

## 🧩 Scenario

During the AWS migration process, some resources became obsolete after alternative solutions were implemented.  
To optimize resource usage and reduce unnecessary infrastructure costs, unused resources must be removed.

In this task, an **EC2 instance** that is no longer required needs to be deleted.

---

# 🎯 Objective

Delete the EC2 instance with the following details:

| Resource | Name |
|--------|------|
| EC2 Instance | `xfusion-ec2` |
| Region | `us-east-1` |

The instance must reach the **Terminated** state before the task is considered complete.

---

# 🧭 Step 1 — Login to AWS Console

1. Open the provided **AWS Console URL**.
2. Sign in using the provided credentials.
3. Ensure the region is set to:
```text
us-east-1 (N. Virginia)
```


You can confirm the region from the **top-right corner** of the AWS Console.

---

# 🖥️ Step 2 — Navigate to EC2 Instances

1. Open the **EC2 Dashboard**.
2. Click:
```text
Instances
```

3. Search for the instance:
```text
xfusion-ec2
```

---

# 🔎 Step 3 — Verify Instance

Confirm the instance details:

| Property | Expected Value |
|---------|----------------|
| Instance Name | `xfusion-ec2` |
| State | Running / Stopped |

If the instance is running, it must still be terminated.

---

# 🗑️ Step 4 — Terminate the Instance

1. Select the instance **xfusion-ec2**.
2. Click **Instance state**.
3. Choose:
```text
Terminate instance
```

4. Confirm the action when prompted.

AWS will now begin terminating the instance.

---

# 🔄 Step 5 — Verify Termination

1. Refresh the **Instances** page.
2. Check the instance state.

Expected status:
```text
Terminated
```

⚠️ It may briefly show **Shutting-down** before reaching **Terminated**.

3. or verify via CLI
```bash
aws ec2 describe-instances \
  --region us-east-1 \
  --filters "Name=tag:Name,Values=xfusion-ec2" \
  --query "Reservations[*].Instances[*].State.Name" \
  --output text
```

---

# ✅ Validation Checklist

- [x] Logged into AWS Console
- [x] Region set to `us-east-1`
- [x] Located instance `xfusion-ec2`
- [x] Instance termination initiated
- [x] Instance state shows **Terminated**

---

# 🏁 Result

The EC2 instance **`xfusion-ec2`** has been successfully deleted and its state is now **Terminated**.

---

# 💡 Key Concepts

- EC2 instance lifecycle states
- Resource cleanup in AWS
- Infrastructure cost optimization
- Safe termination of cloud resources

---

# 📸 Suggested Screenshots (for GitHub Portfolio)

- EC2 Instances page showing `xfusion-ec2`
- Instance state dropdown with **Terminate instance**
- Confirmation prompt
- Instance state showing **Terminated**
