# Internal

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Exploitation, Privilege Escalation |

---

# Objective

Gain initial access to the target machine and escalate privileges to root.

---

# Tools Used

- Nmap
- Gobuster
- WPScan
- Hydra
- SSH
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

Interesting findings included hidden directories leading to a WordPress installation.

## WordPress Enumeration

```bash
wpscan --url http://TARGET_IP
```

Enumerated users and useful WordPress information.

---

# Attack Path

Used WordPress enumeration to identify valid users.

Obtained credentials and authenticated to the target.

Uploaded or executed a reverse shell to gain system access.

---

# Post Exploitation

Performed Linux enumeration.

Used privilege escalation techniques to obtain root access.

Useful commands:

```bash
sudo -l
find / -perm -4000 2>/dev/null
```

---

# Lessons Learned

- WordPress enumeration can reveal valuable attack vectors.
- Hidden directories should always be investigated.
- Thorough Linux enumeration is essential.

---

# Skills Practiced

- WordPress Enumeration
- WPScan
- Reverse Shells
- Linux Privilege Escalation
