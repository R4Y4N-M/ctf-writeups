# Wonderland

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Linux Privilege Escalation |

---

# Objective

Compromise the target machine by obtaining an initial foothold through web enumeration and escalate privileges through multiple Linux privilege escalation techniques until full root access is achieved.

---

# Tools Used

- Nmap
- Gobuster
- SSH
- Linux Terminal
- LinPEAS
- GTFOBins

---

# Enumeration

## Nmap

```bash
nmap -sC -sV TARGET_IP
```

### Findings

- SSH
- HTTP

## Web Enumeration

Performed manual browsing together with directory enumeration to identify hidden application resources.

Useful commands:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration revealed hidden resources that eventually led to valid credentials for the initial foothold.

---

# Attack Path

The machine required careful web enumeration before obtaining valid credentials for SSH access.

Once inside the system, multiple privilege boundaries existed between users. Each privilege escalation stage required additional enumeration and understanding of Linux permissions before progressing to the next user.

Ultimately, local privilege escalation techniques resulted in full root access.

---

# Post Exploitation

Performed standard Linux enumeration.

Useful commands included:

```bash
sudo -l
find / -perm -4000 2>/dev/null
id
getcap -r / 2>/dev/null
```

Several privilege escalation techniques were chained together to reach root.

---

# Lessons Learned

- Enumeration should continue after every privilege change.
- Linux privilege escalation often requires multiple independent techniques.
- GTFOBins is an invaluable reference when auditing privileged binaries.
- Careful inspection of scripts and binaries is essential during post-exploitation.

---

# Skills Practiced

- Web Enumeration
- Linux Enumeration
- SSH
- Privilege Escalation
- GTFOBins
- Post Exploitation

---

# Personal Reflection

Wonderland was one of the most enjoyable rooms I have completed because it emphasized thinking methodically instead of relying on a single exploit. Every privilege escalation stage required a different approach, reinforcing the importance of continuous enumeration and understanding Linux internals.
