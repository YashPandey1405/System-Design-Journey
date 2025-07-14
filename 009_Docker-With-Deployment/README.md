# 🐳 Dockerized Node Deploy

This guide explains how to **Dockerize** a Node.js application and **deploy** it to **AWS Elastic Container Registry (ECR)**.

---

## 📦 What is Dockerizing?

**Dockerizing** refers to the process of converting a local codebase into a **Docker image**, which encapsulates everything your application needs (code, dependencies, env configs) to run identically in any environment.

---

## ☁️ What is AWS ECR?

**Amazon Elastic Container Registry (ECR)** is a fully managed Docker container registry that makes it easy to store, manage, and deploy container images securely.

---

## 🛠️ Step-by-Step: Dockerizing & Pushing to AWS ECR

### 🔧 1. Configure Docker Setup

- Create a `Dockerfile` at the root of your project.
- Add a `.dockerignore` file to exclude unnecessary files from the Docker context.

### 🏗️ 2. Build the Docker Image

```bash
docker build -t node-deploy-app .
```

This command builds the Docker image and tags it as `node-deploy-app`.

### 📂 3. Verify the Image Exists

```bash
docker images
```

You should see `node-deploy-app` listed in the output.

### ▶️ 4. Run the Docker Image (Locally)

**Basic Run:**

```bash
docker run node-deploy-app
```

**Run with Port Mapping:**

```bash
docker run -p 3000:3000 node-deploy-app
```

**Run with Environment Variable:**

```bash
docker run -p 3000:3000 -e PORT=7000 node-deploy-app
```

**Run with `.env` File:**

```bash
docker run -p 3000:3000 --env-file=./.env node-deploy-app
```

---

## 🚀 Deploying to AWS ECR (Simulated Completion ✅)

This section assumes you've successfully deployed the `node-deploy-app` image to AWS ECR.

### ✅ 1. Authenticate Docker to AWS ECR

```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 284818286557.dkr.ecr.ap-south-1.amazonaws.com
```

🟢 _Authentication to ECR successful._

---

### ✅ 2. Build Docker Image (if not already built)

```bash
docker build -t node-deploy-app .
```

🟢 _Docker image `node-deploy-app` built successfully._

---

### ✅ 3. Tag Docker Image for AWS ECR

```bash
docker tag node-deploy-app:latest 284818286557.dkr.ecr.ap-south-1.amazonaws.com/node-deploy-app:latest
```

🟢 _Tagged the image for your ECR repository._

---

### ✅ 4. Push Docker Image to AWS ECR

```bash
docker push 284818286557.dkr.ecr.ap-south-1.amazonaws.com/node-deploy-app:latest
```

🟢 _Image successfully pushed to AWS ECR._

---

## ☁️ AWS Deployment Overview

| Service         | Purpose                                                        |
| --------------- | -------------------------------------------------------------- |
| **ECR**         | Container image registry for pushing and pulling Docker images |
| **ECS**         | Docker orchestration service to deploy and manage containers   |
| **EC2/Fargate** | Compute options to run containers in ECS                       |
| **ALB**         | Load balancer to distribute traffic                            |
| **IAM Roles**   | Secure access to AWS resources                                 |

---

## 🔁 ECS vs EKS

| Feature           | ECS (Elastic Container Service)   | EKS (Elastic Kubernetes Service)             |
| ----------------- | --------------------------------- | -------------------------------------------- |
| **Orchestration** | AWS native Docker orchestrator    | Managed Kubernetes                           |
| **Complexity**    | Easier to set up and use          | More complex, full Kubernetes                |
| **Pricing**       | Lower cost                        | Higher cost due to Kubernetes control plane  |
| **Use Case**      | Best for quick Docker deployments | Best for advanced, Kubernetes-native systems |

> 🧠 **ECS is ideal** for beginners and mid-scale projects who want AWS-managed container deployments.  
> **EKS is preferred** for teams already using Kubernetes.

---

## 🚀 ECS: How It Works

### 1. 📄 Task Definition

- A **Task Definition** is like a blueprint for your containers.
- Includes:
  - Image location from **ECR**
  - CPU and memory specs
  - Network mode (e.g., bridge, awsvpc)
  - IAM Role (controls what the container can access)
  - Environment variables

> 🔐 Tip: Choose **Fargate** (serverless) or **EC2** (self-managed) as your compute type.  
> Fargate = fast and simple, higher cost  
> EC2 = cost-effective but longer provisioning time

---

### 2. 📦 Creating the ECS Cluster

- A **Cluster** is a logical group of EC2 or Fargate resources where your containers run.
- ECS manages container placement within the cluster.

---

### 3. ⚙️ Services and Tasks

- A **Service** defines:
  - Number of desired running **tasks**
  - Load balancer integration
  - Auto scaling (based on CPU/memory)
  - Deployment strategy (rolling, blue/green)

> 💡 You define **Min/Max tasks**, attach a **Security Group**, and optionally use an **Application Load Balancer (ALB)** with a **Target Group** for traffic routing.

---

## 🔧 ECS Step-by-Step Recap

1. **Create Task Definition**

   - Select compute type (EC2/Fargate)
   - Set container specs (RAM, CPU, Image URI from ECR)
   - Define IAM Role

2. **Create Cluster**

   - Acts as the container host group

3. **Create Service**
   - Connects to ALB
   - Sets scaling policy (min/max container count)
   - Manages lifecycle of running containers
