# 🖥️ Day 14 – Enable GUI Boot on All App Servers (Stratos DC)

## 📌 Objective

With the installation of new tools on the app servers within the Stratos Datacenter, certain functionalities now necessitate graphical user interface (GUI) access.

Adjust the default runlevel on all App servers in Stratos Datacenter to enable GUI booting by default.  
**Important:** Do NOT reboot the servers after completing this task.

---

## 🧠 Background

In modern Linux systems (systemd-based), traditional runlevels are replaced by *targets*.

| Old Runlevel | systemd Target |
|-------------|---------------|
| 3 (CLI Mode) | multi-user.target |
| 5 (GUI Mode) | graphical.target |

To enable GUI boot by default, we must set:

```

graphical.target

```

---

## 🛠️ Implementation Steps

### 1️⃣ Login to each App Server

```

ssh tony@stapp01
ssh tony@stapp02
ssh tony@stapp03

```

---

### 2️⃣ Check current default target

```

systemctl get-default

```

If output is:
```

multi-user.target

```
The system is currently set to boot in CLI mode.

---

### 3️⃣ Set GUI as default boot target

```

sudo systemctl set-default graphical.target

```

Expected output:
```

Created symlink ...

```

---

### 4️⃣ Verify configuration

```

systemctl get-default

```

Expected output:
```

graphical.target

```

---

## 🚫 Important Notes

- ❌ Do NOT reboot the server.
- ❌ Do NOT use `systemctl isolate graphical.target`
- ✔ Only change the default target.

---

## ✅ Final Outcome

- All App Servers configured to boot into GUI by default.
- No server reboot performed.
- Configuration persists across reboots.

---

## 🧠 Key Learning

`systemctl set-default graphical.target` changes the boot target permanently without affecting the current session.

---
