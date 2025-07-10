# 🖥️ Linode Bare Metal Deployment Guide (Node.js + PM2 + Caddy)

## 📌 What is a Bare Metal Machine?

A **bare metal machine** is a _dedicated physical server_ that you fully control — no shared resources, no abstraction. You're responsible for everything: the OS, security, deployments, and performance tuning.

### 🔍 Bare Metal vs. Platforms like Vercel/Render

| Feature             | Bare Metal (e.g., Linode)                     | Vercel / Render (PaaS)             |
| ------------------- | --------------------------------------------- | ---------------------------------- |
| **Hardware Access** | Full (physical machine)                       | Abstracted (shared environments)   |
| **Control**         | Root-level access, full customization         | Limited to app-level settings      |
| **Security**        | You manage firewall, SSL, etc.                | Handled mostly by provider         |
| **Scaling**         | Manual (set up load balancers, etc.)          | Auto-scaling out of the box        |
| **Cost**            | Can be more efficient at scale                | Convenient but often pricier       |
| **Performance**     | No noisy neighbors, raw performance           | Good enough for most workloads     |
| **Use Case**        | Custom backend, fine-tuned apps, high traffic | Startups, static sites, prototypes |

---

## 🚀 Bare Metal Deployment on Linode (Node.js Project)

### ✅ Prerequisites

- A working Linode Bare Metal Instance (Ubuntu-based)
- Your project hosted on GitHub (Node.js backend)
- Domain name (optional, for production)

---

### 🧭 Step-by-Step Deployment Instructions

#### 🔧 1. Initial SSH Access

Once the machine is created and running:

```bash
ssh root@<LINODE_IP>
```

Use the localhost name and root password sent via email or Linode dashboard.

---

#### 🔁 2. Update & Install Core Utilities

```bash
apt update && apt install -y curl git
```

---

#### 🌐 3. Install Node.js (v20.x)

First, allow Linux to recognize NodeSource:

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | bash
```

Then install Node.js:

```bash
apt install -y nodejs
```

Verify the installation:

```bash
node -v
```

---

#### 🔁 4. Setup PM2 (Process Manager)

Install PM2 globally:

```bash
npm install -g pm2
```

Then, clone your project and install dependencies:

```bash
git clone https://github.com/<your-username>/<your-project>.git
cd <your-project>
npm install
```

Start your project using PM2:

```bash
pm2 start index.js --name <your-app-name>
```

Enable persistence & startup config:

```bash
pm2 save
pm2 startup
```

---

#### 🌍 5. Install and Configure Caddy Server

**⚠️ Run these commands one by one (as-is). Skipping this will cause issues.**

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | \
sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | \
sudo tee /etc/apt/sources.list.d/caddy-stable.list

chmod o+r /usr/share/keyrings/caddy-stable-archive-keyring.gpg
chmod o+r /etc/apt/sources.list.d/caddy-stable.list

sudo apt update
sudo apt install caddy
```

---

#### ✍️ 6. Configure Reverse Proxy with Caddy

Edit the Caddy configuration:

```bash
nano /etc/caddy/Caddyfile
```

**Insert the following:**

```
yourdomain.com {
    reverse_proxy localhost:3000
}
```

Save the file (`Ctrl + O`, then `Enter`) and exit (`Ctrl + X`).

Then restart Caddy:

```bash
systemctl reload caddy
```

---

### 🌐 7. Access Your App

If your server's IP is `172.105.40.162` and the Node.js app runs on port `3000`, then access it via:

```
https://172.105.40.162:3000/about
```

---

### 📊 8. Monitor Your App

Use PM2 to monitor logs and app health:

```bash
pm2 monit
pm2 logs
```

---

### 🌍 9. Connect Your Domain Name

- Go to your domain registrar (e.g., Namecheap, GoDaddy).
- Add an `A Record` pointing your domain to the Linode machine's public IP.

Example:

| Type | Hostname | Value            | TTL  |
| ---- | -------- | ---------------- | ---- |
| A    | @        | `172.105.40.162` | Auto |

---

### 🔁 10. Update After New GitHub Commits

On code updates:

```bash
cd <your-project>
git pull
npm install
pm2 restart <your-app-name>
```

---

## ✅ Final Tips

- 📡 Use HTTPS in production — Caddy auto-generates SSL for valid domains.
- 🔐 Harden your server (firewall with `ufw`, fail2ban, SSH key login, etc.)
- 🔄 Setup a CI/CD flow using GitHub Actions (optional but recommended).
- 🔁 Schedule backups of your machine and data (Linode supports snapshots).
