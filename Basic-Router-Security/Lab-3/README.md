# Lab 03: Console & VTY Security

## 🎯 Objective
Secure console access by setting a password, enabling encryption, and applying basic security.

---

## 📊 Topology

- **1 Router:** R1
- **1 PC:** PC1 (connected via console cable)

---

## 📋 Tasks

- [x] Connect PC1's RS-232 port to R1's console port
- [x] Use console to configure R1
- [x] Set hostname to R1
- [x] Set enable secret to `cisco`
- [x] Set console password to `ccna`
- [x] Require password for console access
- [x] Check running-config — is it encrypted?
- [x] Enable password encryption and verify
- [x] Save configuration

---

## 💻 Commands Used

```
enable
configure terminal
hostname R1
enable secret cisco
line console 0
password ccna
login
exit
do show running-config | include password
service password-encryption
do show running-config | include password
copy running-config startup-config
```

## 🧠 What I Learned

    Console access must be secured with a password (line console 0).

    login forces the router to ask for a password before allowing console access.

    service password-encryption encrypts console passwords with Type 7.

    Console passwords are included in service password-encryption, unlike enable secret.
