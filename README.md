Here is a clean and well-formatted `README.md` file for setting up and configuring Nginx as a reverse proxy for a Next.js frontend and Node.js backend:

---

Learn Docker 

````markdown
# Nginx Setup for Next.js + Node.js (CareerPilot)

This guide helps you install and configure **Nginx** to serve a **Next.js frontend** and a **Node.js backend API** under a single domain using reverse proxying.

---

## 1. Install & Enable Nginx (Ubuntu/Debian)

Open your terminal and run the following commands:

```bash
sudo apt update
sudo apt install nginx
sudo systemctl enable nginx
sudo systemctl start nginx
````

---

## 2. Create the Nginx Config

Create or update the site configuration file:

```bash
sudo nano /etc/nginx/sites-available/careerpilot
```

Paste the following configuration:

```nginx
server {
    listen 5000;
    server_name localhost;

    # Frontend (Next.js)
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    # Backend (Node.js API)
    location /api/ {
        proxy_pass http://localhost:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

---

## 3. Enable the Config

Link the config file to the `sites-enabled` directory:

```bash
sudo ln -s /etc/nginx/sites-available/careerpilot /etc/nginx/sites-enabled/
```

---

## 4. Test & Reload Nginx

Check for syntax errors and apply the new configuration:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

To stop Nginx on your system, you can use one of the following commands, depending on what exactly you want to do:

---

### 🛑 To **stop** Nginx immediately:

```bash
sudo systemctl stop nginx
```

---

### 🔁 To **restart** Nginx (stop & start again):

```bash
sudo systemctl restart nginx
```

---

### 🔄 To **reload** Nginx config without downtime:

```bash
sudo systemctl reload nginx
```

---

### 🚫 To **disable** Nginx from starting on boot:

```bash
sudo systemctl disable nginx
```

---

### ✅ To **check Nginx status**:

```bash
sudo systemctl status nginx
```

---

Let me know if you want to **completely uninstall** Nginx or **temporarily stop only port 5000** or similar.


## Notes

* Make sure your **Next.js** app is running on port `3000` and your **Node.js API** is running on port `8080`.
* If you want to expose it on port `80` or use a domain name, adjust the `listen` and `server_name` values in the config.
* You can access your app at `http://localhost:5000`

---

```

Let me know if you want a downloadable version or want it adapted for a domain (e.g. with HTTPS via Let's Encrypt).
```
