## 🐳 Docker for Deployment: Study Notes

### 🔧 The Problem with Traditional Deployment (Platform Dependency)

When deploying a Node.js application to an AWS EC2 machine, replicating the same environment across multiple developers' machines can be problematic:

- Developers use different OSes (Windows, Linux, macOS).
- Platform-dependent tools (e.g., `prisma generate`) can behave inconsistently.
- The final merged code might fail during deployment on EC2.

### ❌ Traditional Solution: Oracle Virtual Machines

- A single shared VM could be used for all developers.
- But:

  - VM images are large (\~4GB or more).
  - Managing and scaling VMs is complex and resource-heavy.

> 💀 Scaling using VMs = **God-level pain**

---

### ✅ Better Solution: Docker

- Docker lets you package your app into **images** that contain all dependencies but not the OS.
- The **Docker Host OS** runs containers using its own kernel.
- Lightweight, portable, and consistent across environments.

---

## 🆚 Docker Image vs Container

| **Docker Image**               | **Docker Container**                  |
| ------------------------------ | ------------------------------------- |
| Blueprint (like a class)       | Running instance (like an object)     |
| Read-only template             | Mutable and running                   |
| Used to create containers      | Actual runtime unit of the image      |
| Stored in DockerHub or locally | Created from image using `docker run` |

---

![Alt Text](data:image/jpeg;base64,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FriAhzLSsrrmZ1yMCFWxLdlhA6iYZgASTYDUk8BOKw2Lr06SpUqumISnh1o0TY74lEzZrglzmLIxB6OW+nE52pjGejilas++K41DhwoIFNUqikcoGZQVCMHvqWtzAAdrE5DF7RxK07OwSp5wq1iGy06VBkZqZp1Ch6JKopci+Yv1dLSdgV69WquesTTWmWGW2WpetVRSzFFLWRV1AAOh1gX+IxlOnbPUVLmwzsFuewXOs3zmqtehTxWKOJyDOtMUzVAIeiEsaaXHSO83hKjXpDTUSI2NZBlV6lFlXDjC4d7XdSq3VwQWc3LI2vRC304kOwMxecjUauaN2rVGNWliwwsoC5b7vJZbggad9+ekjNthlekErEqrYRLO69OnU3Wd1QId4tnN6hZQCpHLUO2VweBv4d2hnqcca9criCKrpuqVeogRUAaouIxIW4y69FE053v3z3hdpYhsVlZwDvnU0s1zuQrZW3Yp3AICtnL2ubf5YHXRKvya3hwtB6rs9R6aVHLgAhmRSQAALAdktICIiAmLTMQMWi0zEDFpm0RAxaZiICIiAiIgJi0zEDFotMxAxaZiIC0xaZiBBw2yaSPnAbN0rZndlTNq2RWJCX7gJOtEQEREBERAxaLTMQMWmbREDFotMxAxaLTMQMWi0zEBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQEREBERAREQERED//2Q==)
![Alt Text](data:image/png;base64,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)

---

## 🐳 Docker Basics

### 🔽 Pull and Run an Image

```bash
docker run ubuntu sleep 10
```

- Pulls the Ubuntu image (if not already available locally)
- Runs it and executes `sleep 10` inside it

### 🧹 Auto-remove container after execution

```bash
docker run --rm ubuntu sleep 10
```

- `--rm`: container will be removed after completion

---

## 🛠️ Common Docker Commands

| Command                               | Description                   |
| ------------------------------------- | ----------------------------- |
| `docker run <image>`                  | Run a container from image    |
| `docker run -it <image>`              | Interactive terminal access   |
| `docker run --rm <image>`             | Auto-remove after run         |
| `docker ps`                           | List running containers       |
| `docker ps -a`                        | List all containers           |
| `docker stop <container_id>`          | Stop a running container      |
| `docker start <container_id>`         | Start a stopped container     |
| `docker exec -it <container_id> bash` | Enter running container shell |
| `docker images`                       | List local images             |
| `docker rmi <image_id>`               | Remove a Docker image         |
| `docker rm <container_id>`            | Remove a container            |
