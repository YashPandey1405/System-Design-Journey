# ⚙️ AWS Practical Notes – Deployment, DB & Auto Scaling

_By Yash Pandey_

---

## ✅ Use Case:

**Domain**: https://YashPandey029/about.com  
**Users**: ~500  
**Bandwidth**: 2000GB/month  
**Stack**: React + Node.js + MongoDB + AWS Infra

---

## 1️⃣ How Do I Deploy My Site with Auto Scaling?

- Use **Launch Template** with **User Data script** to auto-deploy code.
- Example:

  ```bash
  #!/bin/bash
  apt update
  apt install -y git nodejs npm
  git clone <repo>
  cd repo && npm install && npm start
  ```

- Each EC2 instance launched auto-runs this on boot.
- Load Balancer routes traffic to these instances.

**Flow**:

```
Domain → Load Balancer → Target Group → EC2 (Auto Scaling) → App
```

---

## 2️⃣ MongoDB: Atlas vs EC2 Hosting?

| Option      | MongoDB Atlas              | EC2 Self-Host           |
| ----------- | -------------------------- | ----------------------- |
| Setup       | Managed                    | Manual                  |
| Cost        | Free tier (500MB)          | EC2 & EBS charges       |
| Security    | TLS, built-in              | You configure           |
| Integration | Easy (via URI + whitelist) | Private VPC possible    |
| Best For    | Startups, simplicity       | Full control + practice |

🔗 Yes, you can integrate **MongoDB Atlas with AWS EC2** (use `.env` with connection URI).

---

## 3️⃣ How Does Auto-Scaling Scale In (Down)?

**Scenario**:

- Min EC2s: `2`, Max: `10`
- Load spikes → 9 EC2s started
- After 30 mins, traffic drops

**What Happens**:

1. CloudWatch sees low CPU/traffic
2. ASG waits for cooldown (default 300s)
3. Gradually terminates EC2s
4. Stops at `min = 2` machines

✔️ Load Balancer handles deregistration before shutdown
✔️ Grace periods prevent premature kills

---

## 🧠 Quick Tips:

- Use **User Data** for zero-touch deploys
- Start with **MongoDB Atlas Free Tier**, migrate later if needed
- Monitor with **CloudWatch**, scale with **Target Tracking**

---

## 📌 **Stack Used**:
EC2, Auto Scaling Group, Load Balancer, MongoDB Atlas, CloudWatch, Launch Template
