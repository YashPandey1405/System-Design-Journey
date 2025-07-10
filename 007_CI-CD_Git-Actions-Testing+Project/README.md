# 🚀 CI/CD Pipeline with GitHub Actions & Automated Testing using Jest & Supertest

> **Made with 💻, ☕, and GitHub Actions by Yash Pandey**

---

## 📖 Table of Contents

- [🔧 What is CI/CD?](#-what-is-cicd)
- [🤖 What is GitHub Actions?](#-what-is-github-actions)
- [🧪 Unit Testing using Jest & Supertest](#-unit-testing-using-jest--supertest)
- [📜 Final Notes](#-final-notes)

---

## 🔧 What is CI/CD?

**CI/CD** stands for **Continuous Integration** and **Continuous Deployment**.

- 🧩 **CI (Continuous Integration)**: Automatically integrates code changes, runs tests, and builds the project whenever code is pushed.
- 🚀 **CD (Continuous Deployment)**: Automatically deploys the latest working code to production or a hosting service once tests pass.

This ensures:

- Fast feedback on code issues
- Cleaner code merges
- Automated deployment without manual intervention

---

## 🤖 What is GitHub Actions?

**GitHub Actions** allows you to **automate workflows** like testing, building, and deployment **directly from your GitHub repository**.

### Example Workflows:

- Run tests on every push to `main`
- Deploy code automatically to Render, Vercel, etc.
- Lint or format code on pull requests

In this project, **GitHub Actions** runs tests with every push to `main` and **only deploys** if tests pass successfully.

---

## 🧪 Unit Testing using Jest & Supertest

### 🔍 **Jest**

- A JavaScript testing framework for writing and running unit tests.
- Offers assertions like `expect(value).toBe(…)`.

### 🌐 **Supertest**

- Used for testing **HTTP APIs**.
- Allows sending fake requests to your Express routes without starting the server.

Together, these tools ensure:

- Your API routes behave as expected.
- Changes don’t break existing functionality.

---

## 📜 Final Notes

This project demonstrates a **simple but complete CI/CD workflow** with testing and deployment automation.
It’s ideal for beginners who want to:

- Understand real-world CI/CD practices
- Learn GitHub Actions basics
- Use Jest & Supertest for Express.js testing

---

> **Made with 💥 CI/CD + GitHub Actions + Testing** by **Yash Pandey**
