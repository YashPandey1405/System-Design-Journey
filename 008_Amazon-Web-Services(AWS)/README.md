## 🌩️ Amazon Web Services (AWS) - Core Concepts & Deployment Insights

### 🟨 What is AWS?

Amazon Web Services (AWS) is a leading cloud service provider offering scalable, reliable, and cost-efficient infrastructure for deploying and managing applications.

### 🟢 Other Cloud Providers

- **Azure** – Microsoft’s cloud platform.
- **Digital Ocean** – Developer-friendly, simplified cloud infrastructure.

---

### ✅ Benefits of AWS

- **Flexibility**: Choose services as per need.
- **Scalability**: Auto-scaling based on demand.
- **Storage Access**: Reliable and fast object/file storage.
- **Fault Tolerance**: Handles failure gracefully.
- **High Performance**: Globally distributed data centers.
- **Security**: Fine-grained access control, encryption.

---

### ❌ Downsides of AWS

- **High Compute Costs**
- **Expensive Storage (esp. S3 with high usage)**
- **Costly Data Outflow (Egress traffic)**

---

## 🔐 Identity and Access Management (IAM)

### 👤 IAM Users

- Represent **individual people or applications**.
- Each user has **access keys or login credentials**.
- We can assign **fine-grained permissions** using **IAM Policies**.
- **Least Privilege Principle**: Grant only required permissions.

### 👥 IAM Groups in Production

- Group users by **roles/departments** (e.g., DevOps, Frontend, QA).
- Attach **policies to groups**, not individuals.
- Example:

  - Group: `DevOpsTeam`
  - Permissions: Full EC2 & CloudWatch access
  - All members of this group inherit those permissions

---

## 🧠 Core AWS Services

### 🔹 `EC2` – Elastic Compute Cloud

> Provision virtual machines (instances) to run applications.

### 🔹 `S3` – Simple Storage Service

> Store and retrieve any amount of data at any time, securely and reliably.

### 🔹 `ELB` – Elastic Load Balancer

> Distributes incoming traffic across multiple EC2 instances.

> **Note:** “Elastic” in AWS usually implies cost increase due to auto-scaling or traffic handling.

![ELB + ASG](https://camo.githubusercontent.com/c6bd4c9eed6167a370d6e45350a739bad63058b102d18b3db4eb3abf1b0cd61d/68747470733a2f2f7265732e636c6f7564696e6172792e636f6d2f646168376c3875746c2f696d6167652f75706c6f61642f76313735313837353535302f57686174734170705f496d6167655f323032352d30372d30375f61745f31332e33322e32385f33613365613930355f64766f676d612e6a7067)
![ELB + ASG](https://media.tutorialsdojo.com/AWS-ELB-ASG.png)

---

## 🎯 Target Group + Load Balancer Flow

A **Target Group** is a set of EC2 instances that handle requests forwarded by the ELB.

### 🔗 Real-world Domain Configuration

```text
Your Domain DNS (A Record)
        ↓
Load Balancer DNS (AWS provided)
        ↓
Target Group
        ↓
EC2 Instances
```

![Domain to EC2](https://jayendrapatil.com/wp-content/uploads/2016/04/screen-shot-2016-04-05-at-7-54-34-am.png)

---

## 📈 Auto Scaling Group (ASG)

Auto Scaling enables **automatic launching or termination of EC2 instances** based on CPU load or custom metrics.

### Example Trigger:

```text
If CPU Utilization > 80% → Spin up a new EC2
```

### ⚖️ Optimal Thresholds:

- **80%**: May crash if traffic spikes suddenly
- **60%**: Safer but may underutilize & increase cost

> Always define thresholds based on **business logic** and expected user load.

### 🛠️ ASG Automation:

- Automatically adds new EC2 to the **Target Group** — no manual intervention.
- Set:

  - **Minimum Instances**: Always running (e.g., 2)
  - **Maximum Instances**: Upper bound (e.g., 10)

- Attach **launch scripts** for setup:

  ```bash
  git clone <repo>
  npm install
  ```

### 🧹 ASG Deletion (Production Practice)

1. Set **minimum EC2s = 0**
2. Then **delete the Auto Scaling Group**

---

## 🛠️ Other AWS Services (Quick View)

| Service               | Use Case                                            |
| --------------------- | --------------------------------------------------- |
| **Elastic Beanstalk** | Easy deployment of web apps (JS, Java, Python, PHP) |
| **AWS LightSail**     | Simplified VM hosting (like Linode, DigitalOcean)   |
| **CloudWatch**        | Logs, metrics, alerts, billing monitors             |

---

## 💸 AWS Billing Optimization Tips

- **Reserve Instances**:

  - Commit usage for **1–3 years** → Get **major discounts**
  - Applies to:

    - EC2
    - Storage
    - Auto Scaling
    - Load Balancers

---

## 📚 Summary Flow

```text
Users → Route to Domain DNS → ELB (DNS Provided by AWS)
→ Target Group → EC2 Instances (Auto-scaled based on Load)
→ Logs & Alerts → CloudWatch
```

---

## 🔚 Final Thoughts

Understanding core AWS services like EC2, ELB, ASG, S3, and IAM is essential for scalable and production-ready application deployment. Combine them wisely for performance, availability, and cost efficiency.
