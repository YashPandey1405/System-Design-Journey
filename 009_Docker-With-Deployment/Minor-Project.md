# 🐳 Dockerized Node Deploy on AWS 🚀

A hands-on mini project where I learned the **end-to-end containerization and deployment** workflow using **Docker**, **AWS ECR**, and **AWS ECS**.

➡️ [View the Project Repo](https://github.com/YashPandey1405/Dockerized-Node-Deploy)

---

## 📦 What I Learned

- Docker fundamentals: building and running images
- Image tagging, pushing to AWS Elastic Container Registry (ECR)
- Deploying containerized apps using AWS Elastic Container Service (ECS)
- Working with Clusters, Task Definitions, Services, and Load Balancers on AWS
- Orchestrating containers using ECS (EC2/Fargate launch types)
- Configuring IAM roles, auto-scaling, and container security

---

## 🐳 Docker Concepts Practiced

| Step          | Command                                           | Purpose                      |
| ------------- | ------------------------------------------------- | ---------------------------- |
| Build Image   | `docker build -t node-deploy-app .`               | Create image from Dockerfile |
| Run Container | `docker run -p 3000:3000 node-deploy-app`         | Run locally and map ports    |
| Tag Image     | `docker tag node-deploy-app:latest <aws-ecr-uri>` | Tag for pushing to ECR       |
| Push Image    | `docker push <aws-ecr-uri>`                       | Upload to AWS ECR            |
| Env Usage     | `docker run --env-file=.env node-deploy-app`      | Inject environment variables |

---

## ☁️ AWS Deployment Workflow

### 🔐 AWS ECR (Elastic Container Registry)

1. **Authenticate Docker with ECR**

   ```bash
   aws ecr get-login-password --region ap-south-1 | \
   docker login --username AWS --password-stdin 284818286557.dkr.ecr.ap-south-1.amazonaws.com
   ```

2. **Build Docker Image**

   ```bash
   docker build -t node-deploy-app .
   ```

3. **Tag the Image**

   ```bash
   docker tag node-deploy-app:latest 284818286557.dkr.ecr.ap-south-1.amazonaws.com/node-deploy-app:latest
   ```

4. **Push Image to ECR**

   ```bash
   docker push 284818286557.dkr.ecr.ap-south-1.amazonaws.com/node-deploy-app:latest
   ```

---

### ⚙️ AWS ECS (Elastic Container Service)

1. **Task Definition**

   - Define how your Docker image runs (RAM, CPU, ECR image URI, roles).
   - Choose **Fargate** (serverless) or **EC2** (cost-effective) compute type.
   - ECS pulls image directly from ECR.

2. **Cluster Creation**

   - Create an ECS cluster (logical group of machines for orchestration).

3. **Service Configuration**

   - Define desired number of containers.
   - Attach Security Groups and IAM Roles.
   - Add Auto Scaling rules (based on CPU/Memory).
   - Integrate with Application Load Balancer and Target Groups.

---

## 🔁 ECS vs EKS (Quick Comparison)

| Feature    | ECS               | EKS                    |
| ---------- | ----------------- | ---------------------- |
| Platform   | AWS-native        | Kubernetes (Managed)   |
| Cost       | Lower             | Higher                 |
| Complexity | Beginner-friendly | Advanced setup         |
| Use Case   | Small/Medium apps | Kubernetes-heavy teams |

---

## 📌 Highlights

- 🐳 Docker-based microservice setup
- 🔐 Secure ECR image push and pull
- ☁️ ECS cluster orchestration
- 📈 Auto-scaling with ALB and Task Services

---

> Built with ☁️ Docker + AWS ECR/ECS by **Yash Pandey** > [GitHub Repo](https://github.com/YashPandey1405/Dockerized-Node-Deploy)
