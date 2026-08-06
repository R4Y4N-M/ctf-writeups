# Mr. Robot

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Exploitation |

---

# Objective

Compromise the target system and obtain root access.

---

# Tools Used

- Nmap
- Gobuster
- WPScan
- Burp Suite
- Netcat
- Linux Terminal

---

# Enumeration

## Nmap

```bash
nmap -sC -sV TARGET_IP
```

Discovered:

- HTTP
- SSH

## Directory Enumeration

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Discovered hidden directories and WordPress resources.

---

# Attack Path

Enumerated the website and gathered useful information.

Obtained credentials through enumeration.

Gained access to the target and established a reverse shell.

---

# Post Exploitation

Performed local enumeration.

Escalated privileges through Linux misconfigurations.

---

# Lessons Learned

- Enumeration often provides multiple attack paths.
- WordPress environments expose many opportunities when misconfigured.
- Local enumeration should never be skipped.

---

# Skills Practiced

- WordPress Enumeration
- Burp Suite
- Reverse Shells
- Linux Enumeration
