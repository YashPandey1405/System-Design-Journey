# 📡 RealTime-Kafka-Microservice

A real-time microservice project demonstrating **Apache Kafka** in action — built to model how scalable producer-consumer systems communicate with partitioned topics and consumer groups.

## 🧠 What is Apache Kafka?

Apache Kafka is a **distributed event streaming platform** used to build real-time data pipelines and streaming applications. It is designed for **high-throughput, fault-tolerant, scalable** messaging.

Use cases include:

- Real-time analytics
- Microservice communication
- Activity tracking
- Log aggregation
- Event-driven systems

---

## 📦 Project Architecture

### 🛠 Components:

- **Producer**: Accepts input via a form and sends data to Kafka topics.
- **Kafka Topics**:
  - `rider-updates` → 2 partitions
  - `hotel-updates` → 2 partitions
- **Consumers**:
  - Group 1 → Subscribed to `rider-updates` with 2 consumers → Each gets 1 partition.
  - Group 2 → Subscribed to `hotel-updates` with 1 consumer → Handles both partitions.

![Architecture Overview](https://res.cloudinary.com/dah7l8utl/image/upload/v1752086859/Screenshot_2025-07-10_001721_dwqfdf.png)

---

## 🧪 Tech Stack

- **Apache Kafka**
- **Node.js** (KafkaJS)
- **Express**
- **Cloudinary** (for demo screenshots)

---

## 🔗 Related System Design Projects

➡️ [Apache-Kafka Project](https://github.com/YashPandey1405/RealTime-Kafka-Microservice)

---

Made with 🧠 + ⚙️ by **Yash Pandey**
