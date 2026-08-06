# Lab 01: Basic Router Security 1

## 🎯 Objective
Secure two routers with basic password configuration, enable password encryption, and test the effect of `service password-encryption`.

---

## 📊 Topology

- **2 Routers:** R1, R2
- **Connection:** GigabitEthernet0/0 between R1 and R2

---

## 📋 Tasks

- [x] Connect R1 and R2 using GigabitEthernet0/0
- [x] Set hostnames to R1 and R2
- [x] Set enable password to `cisco`
- [x] View password in running-config (not encrypted)
- [x] Enable password encryption
- [x] View password again (now encrypted)
- [x] Disable password encryption
- [x] View password again (plain text again)

---

## 💻 Commands Used

```
enable
configure terminal
hostname R1
enable password cisco
do show running-config | include enable password
service password-encryption
do show running-config | include enable password
no service password-encryption
do show running-config | include enable password
```

## 🧠 What I Learned

    enable password is stored in plain text by default.

    service password-encryption encrypts passwords but uses Type 7 (weak encryption).

    Disabling encryption reverts passwords to plain text.

    enable secret (not used here) is stronger and uses Type 5 (MD5).
