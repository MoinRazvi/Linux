# 🔐 Day 13 – Crontab Access Restriction (Linux Security Hardening)

## 📌 Topic

**Restricting Crontab Access Using cron.allow (Nautilus Project – Stratos DC)**

---

## 🎯 Objective

In alignment with security compliance standards, the Nautilus project team has opted to impose restrictions on crontab access. Specifically, only designated users will be permitted to create or update cron jobs.

**Task Requirement (Day-13):**
Configure crontab access on **App Server 3** as follows:

* ✅ Allow crontab access to **anita** user
* ❌ Deny crontab access to **ryan** user

---

## 🧠 Background

Linux controls user access to scheduled jobs through two configuration files:

* `/etc/cron.allow` → **Whitelist**
* `/etc/cron.deny` → **Blacklist**

### 🔑 Important Rule

> If `/etc/cron.allow` exists, **only users listed in it can access crontab**.
> All other users are denied by default, regardless of `cron.deny`.

For security compliance, **cron.allow** is the preferred approach.

---

## 🛠️ Implementation Steps

### 1️⃣ Login to App Server 3

```bash
ssh tony@stapp03
```

---

### 2️⃣ Create or edit the cron.allow file

```bash
sudo vi /etc/cron.allow
```

Add **only** the allowed user:

```text
anita
```

Save and exit.

---

### 3️⃣ Ensure ryan is denied

No additional action is required for `ryan` as long as:

* `ryan` is **not listed** in `/etc/cron.allow`

(Optional cleanup)

```bash
sudo sed -i '/^ryan$/d' /etc/cron.deny 2>/dev/null
```

---

## 🔍 Verification

### Check allowed users

```bash
sudo cat /etc/cron.allow
```

Expected output:

```text
anita
```

---

### Validate access behavior

**As anita (allowed):**

```bash
su - anita
crontab -l
```

✅ Access granted

**As ryan (denied):**

```bash
su - ryan
crontab -l
```

❌ Access denied

**As any other user (example: banner):**

```bash
crontab -l
```

❌ Access denied (expected)

---

## ✅ Final Outcome

* ✔ `anita` can create and manage cron jobs
* ❌ `ryan` is denied crontab access
* 🔐 All non-authorized users are restricted
* 📋 Security compliance requirements satisfied

---

## 🧠 Key Learnings

* `cron.allow` enforces **strict user-level cron control**
* Whitelisting is more secure than blacklisting
* Presence of `cron.allow` overrides all cron access rules

---
