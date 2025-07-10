# ⚙️ PM2: Process Manager for Node.js Applications

## 📌 What is PM2?

**PM2** is a **production-grade process manager** for Node.js applications. It ensures that your apps:

- Stay alive (auto-restarts on crashes)
- Are monitored in real time
- Can be gracefully stopped or restarted
- Run in the background as daemons (independent of terminal sessions)

Think of PM2 as your **Node.js app babysitter** — it keeps your apps running and healthy.

---

## 🚀 Why Use PM2?

Here’s why PM2 is essential for Node.js deployment on bare metal servers or cloud VMs:

| Feature               | Description                                                                 |
| --------------------- | --------------------------------------------------------------------------- |
| 🔁 Auto-Restart       | Automatically restarts app if it crashes or your server reboots             |
| 🧠 Process Management | Manage multiple apps with a single tool                                     |
| 📈 Monitoring         | Real-time CPU, memory usage, logs, and status tracking                      |
| 🧹 Log Aggregation    | Access all stdout/stderr logs in one place                                  |
| 💾 Boot Persistence   | Your apps restart automatically even after a machine reboot (`pm2 startup`) |
| 📦 Clustering         | Supports multi-core usage using Node.js cluster module                      |

---

## 📦 Installing PM2

```bash
npm install -g pm2
```

---

## 🛠️ Basic PM2 Usage

### 🔹 Start your app

```bash
pm2 start index.js --name my-app
```

> Replace `index.js` with your entry file and `my-app` with a custom process name.

---

### 🔹 Show running apps

```bash
pm2 list
```

---

### 🔹 View logs (stdout + stderr)

```bash
pm2 logs
```

---

### 🔹 Monitor usage (CPU, memory, uptime)

```bash
pm2 monit
```

---

### 🔹 Restart / Stop / Delete app

```bash
pm2 restart my-app
pm2 stop my-app
pm2 delete my-app
```

---

## 💾 Save & Auto-Restart on Reboot

1. **Save running processes:**

   ```bash
   pm2 save
   ```

2. **Setup auto-startup script:**

   ```bash
   pm2 startup
   ```

   Then copy-paste the command PM2 gives you to enable it.

---

## 📁 Where Are Logs Stored?

By default:

- **stdout logs:** `~/.pm2/logs/my-app-out.log`
- **stderr logs:** `~/.pm2/logs/my-app-error.log`

---

## 🧠 Bonus: Running Multiple Apps

```bash
pm2 start app1.js --name api-server
pm2 start app2.js --name job-worker
```

You can also start apps with an ecosystem config file (`ecosystem.config.js`) for more control.

---

## 🔒 Tip for Production

- Use **PM2 + Caddy or Nginx** for reverse proxy and HTTPS
- Combine PM2 with **Git pull + restart script** for easy updates
- Keep your `.env` files secure; avoid committing sensitive values

---

## ✅ Summary

| PM2 Benefit       | Why it matters                          |
| ----------------- | --------------------------------------- |
| Auto-Restart      | No downtime due to crashes or reboots   |
| Logs & Monitoring | Easy debugging and performance tracking |
| Simple Commands   | Manage complex apps with ease           |
| Boot Persistence  | No need to manually restart apps        |
