# 🏗️ System Design – Scalable, Resilient & Real-World Ready

This document covers the essential and advanced concepts of **System Design** used in real-world production systems. Whether you're preparing for interviews or building distributed apps, this is your one-stop guide.

---

## 📌 Table of Contents

1. [Client-Server Architecture](#1-client-server-architecture)
2. [Read & Write Databases](#2-read--write-databases)
3. [Auto-Scaling in Cloud (AWS)](#3-auto-scaling-in-cloud-aws)
4. [Load Balancing Strategies](#4-load-balancing-strategies)
5. [Vertical vs Horizontal Scaling](#5-vertical-vs-horizontal-scaling)
6. [DDoS Attacks & Prevention](#6-ddos-attacks--prevention)
7. [Caching, Queues & CDNs](#7-caching-queues--cdns)
8. [Eventual vs Strong Consistency](#8-eventual-vs-strong-consistency)
9. [Best Practices & Real-World Example](#9-best-practices--real-world-example)
10. [Architecture Screenshot](#10-architecture-screenshot)

---

## 1️⃣ Client-Server Architecture

In a production-grade web application:

- **Clients**: Frontend (web/mobile apps)
- **Servers**: Handle client requests, API logic, authentication, etc.
- **Databases**: Persistent storage
- **Middlewares**: Auth, logging, monitoring, etc.

---

## 2️⃣ Read & Write Databases

- **Primary Database** handles all **read/write operations**.
- **Read Replicas** are 2–3 additional instances for **read-only** queries.
- Helps in:
  - Reducing load on the main DB
  - Handling analytics/dashboard traffic
  - Faster reads for distributed users

> 🔁 Read replicas are **eventually consistent**. They sync periodically with the main DB based on business logic.

---

## 3️⃣ Auto-Scaling in Cloud (AWS)

### 🔼 Upscaling:

- Enabled via **AWS Auto Scaling Group (ASG) + Elastic Load Balancer (ELB)**.
- If CPU > 80%:
  - A **new EC2 instance** spins up
  - Bootstraps in ~5–10s
  - Traffic is distributed evenly

### 🔽 Downscaling:

- When load drops:
  - Idle servers (0 users) are scheduled for shutdown
  - AWS waits until **all active requests complete**
  - Graceful shutdown ensures no request is dropped

---

## 4️⃣ Load Balancing Strategies

- **Round Robin** – Circular assignment
- **Least Connections** – Smart routing to least busy server
- **IP Hash** – Routes based on client IP

🔧 Tools:

- NGINX
- HAProxy
- AWS ELB
- Cloudflare Load Balancer

---

## 5️⃣ Vertical vs Horizontal Scaling

| Type       | Scaling Method                   | Example             | Tradeoffs                      |
| ---------- | -------------------------------- | ------------------- | ------------------------------ |
| Vertical   | Increase resources on one server | t2.micro → t2.large | Hardware limit                 |
| Horizontal | Add more servers                 | Add more EC2s       | Needs orchestration (ELB, K8s) |

---

## 6️⃣ DDoS Attacks & Prevention

### 🚨 What is DDoS?

> Distributed Denial of Service (DDoS) floods your server with fake traffic from multiple machines.

### 🛡️ Protection Techniques:

- **Cloudflare / Akamai** – Block at the edge
- **WAF** – Block malicious patterns (SQLi, XSS)
- **Rate Limiting** – Requests per second/IP
- **Auto Scaling** – Absorb traffic temporarily
- **Geo/IP Blocking** – Deny traffic from suspicious regions

---

## 7️⃣ Caching, Queues & CDNs

### 🧠 Smart Performance Boosters:

- **Redis / Memcached** – Cache frequent data
- **Kafka / RabbitMQ** – Handle write-heavy workflows
- **CDNs (Cloudflare, Fastly)** – Serve static assets closer to users

---

## 8️⃣ Eventual vs Strong Consistency

| Consistency Type | Description           | Use Cases               |
| ---------------- | --------------------- | ----------------------- |
| Strong           | Latest data always    | Banking, Payments       |
| Eventual         | May return stale data | Analytics, Social Feeds |

---

## 9️⃣ Best Practices & Real-World Example

- ✅ **Graceful shutdowns**: Wait for pending requests
- ✅ **Keep services stateless**: Easy to scale horizontally
- ✅ **Pre-warm servers**: Avoid cold starts
- ✅ **CDN & Cache usage**: Faster user experience
- ✅ **Monitoring & Logging**: Use Grafana, ELK, or CloudWatch

### 🧩 Sample System Flow:

```

User → Load Balancer → Web Servers (Auto-scaled EC2s) →
Redis Cache & DB → Read Replicas
↓
CDN (for static content)

```

---

## 🖼️ 10. Architecture Screenshot

Below is a visual representation of the auto-scaling and load-balancing mechanism in action:

![System Design Screenshot](https://res.cloudinary.com/dah7l8utl/image/upload/v1751870216/Screenshot_2025-07-07_115406_xa4302.png)

> This screenshot shows AWS ELB routing requests to multiple EC2s, with auto-scaling based on CPU utilization.

---

## 📚 Final Thoughts

System Design is not just about scale — it's about:

- **Reliability**
- **Performance**
- **Security**
- **Cost efficiency**

Mastering these concepts helps you build production-ready applications that perform under real-world stress and traffic.

---

**Made with 💻 by Yash Pandey | Web Developer & Data Scientist**
