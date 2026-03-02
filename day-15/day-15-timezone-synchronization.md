## 📌 Objective

In the daily standup, it was noted that the timezone settings across the Nautilus Application Servers in the Stratos Datacenter were inconsistent with the local datacenter timezone.

The local datacenter timezone is set to:

Pacific/Chatham

Synchronize the timezone settings on all Nautilus Application Servers to match this timezone.

⚠️ No server reboot should be performed.

---

## 🧠 Background

Linux systems using systemd manage time and timezone configuration through:

timedatectl

Timezone changes made using `timedatectl`:
- Apply immediately
- Persist across reboots
- Do not require system restart

---

## 🛠️ Implementation Steps

### 1️⃣ Login to each App Server

```

ssh tony@stapp01
ssh tony@stapp02
ssh tony@stapp03

```

---

### 2️⃣ Verify Available Timezones (Optional)

```

timedatectl list-timezones | grep Pacific/Chatham

```

Expected output:
```

Pacific/Chatham

```

---

### 3️⃣ Set the Timezone

```

sudo timedatectl set-timezone Pacific/Chatham

```

---

### 4️⃣ Verify the Change

```

timedatectl

```

Expected output should include:
```

Time zone: Pacific/Chatham

```

---

## ✅ Validation Checklist

- ✔ Timezone set to Pacific/Chatham
- ✔ No reboot performed
- ✔ Change reflected immediately
- ✔ Configuration persists across reboots

---

## 🧠 Key Learning

- `timedatectl` is the modern tool for timezone management.
- Timezone configuration is stored system-wide and survives reboot.
- No service restart is required after changing timezone.

---

