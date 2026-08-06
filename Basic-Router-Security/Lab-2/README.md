
# Lab 02: Basic Router Security 2

## 🎯 Objective
Compare `enable password` vs `enable secret`, understand which one takes priority.

---

## 📊 Topology

- **2 Routers:** R1, R2
- **Connection:** GigabitEthernet0/0 between R1 and R2

---

## 📋 Tasks

- [x] Connect R1 and R2 using GigabitEthernet0/0
- [x] Set hostnames to R1 and R2
- [x] Set enable password to `cisco`
- [x] Set enable secret to `ccna`
- [x] Exit to exec mode and try to enter privileged exec mode
- [x] Which password did you use?
- [x] View running-config — which password is encrypted?
- [x] Enable password encryption and check what changed
- [x] Save configuration and reload to confirm

---

## 💻 Commands Used

```
enable
configure terminal
hostname R1
enable password cisco
enable secret ccna
exit
enable
do show running-config | include enable
service password-encryption
do show running-config | include enable
copy running-config startup-config
reload
```


## 🧠 What I Learned

    When both enable password and enable secret are set, enable secret takes priority.

    enable secret uses Type 5 (MD5) encryption, which is stronger.

    service password-encryption does NOT encrypt enable secret.
