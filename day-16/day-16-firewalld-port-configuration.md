# 🔥 Day 15 – Firewalld Configuration for Backup Web UI (Port 8089)

## 📌 Objective

The Nautilus system admins team has deployed a web UI application for their backup utility on the Nautilus Backup Server within the Stratos Datacenter.

The application runs on:

Port: 8089/tcp

Since `firewalld` is active on the server, the following requirements must be met:

- Allow all incoming connections on port 8089/tcp
- Ensure the firewall zone is set to `public`
- Make the configuration persistent

---

## 🧠 Background

`firewalld` is a dynamic firewall management tool in RHEL/CentOS-based systems.

Key concepts:

- Zones define trust levels (public, internal, trusted, etc.)
- Permanent changes require `--permanent`
- Firewall must be reloaded after permanent changes

---

## 🛠️ Implementation Steps

### 1️⃣ Login to the Backup Server

```

ssh clint@stbkp01

```

---

### 2️⃣ Verify firewalld is running

```

sudo systemctl status firewalld

```

If not running:

```

sudo systemctl start firewalld
sudo systemctl enable firewalld

```

---

### 3️⃣ Set the default zone to public

```

sudo firewall-cmd --set-default-zone=public

```

Verify:

```

sudo firewall-cmd --get-default-zone

```

Expected output:

```

public

```

---

### 4️⃣ Allow port 8089/tcp permanently

```

sudo firewall-cmd --permanent --zone=public --add-port=8089/tcp

```

---

### 5️⃣ Reload firewall to apply changes

```

sudo firewall-cmd --reload

```

---

### 6️⃣ Verify port configuration

```

sudo firewall-cmd --zone=public --list-ports

```

Expected output:

```

8089/tcp

```

---

## ✅ Validation Checklist

- ✔ firewalld is active
- ✔ Default zone is set to `public`
- ✔ Port 8089/tcp is allowed
- ✔ Configuration persists across reboots

---

## 🧠 Key Learning

- Always use `--permanent` for persistent firewall rules.
- Always reload firewall after making permanent changes.
- Verify using `--list-ports` before considering the task complete.

---
