# Road

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Application Exploitation, Linux Privilege Escalation |

---

# Objective

Gain initial access to the target machine through web application vulnerabilities and escalate privileges to obtain full administrative control.

---

# Tools Used

- Nmap
- Gobuster
- Burp Suite Community
- Linux Terminal
- Netcat
- LinPEAS

---

# Enumeration

## Nmap

```bash
nmap -sC -sV TARGET_IP
```

### Findings

- HTTP service
- SSH service

## Web Enumeration

Performed manual browsing together with directory enumeration.

Useful command:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration revealed web application functionality that became the primary attack surface.

---

# Attack Path

The engagement began with web application enumeration, leading to the discovery of weaknesses that allowed unauthorized access to the application.

After gaining initial system access, Linux enumeration identified privilege escalation opportunities that ultimately resulted in root access.

---

# Post Exploitation

Performed standard Linux enumeration.

Useful commands included:

```bash
sudo -l
find / -perm -4000 2>/dev/null
getcap -r / 2>/dev/null
id
```

Enumeration identified local privilege escalation opportunities that were successfully leveraged to obtain root access.

---

# Lessons Learned

- Web applications should always be thoroughly enumerated before exploitation.
- Small web application weaknesses can lead to complete operating system compromise.
- Linux privilege escalation requires continuous enumeration after every privilege change.
- Reviewing permissions and privileged binaries is essential.

---

# Skills Practiced

- Web Enumeration
- Burp Suite
- Linux Enumeration
- Privilege Escalation
- Post Exploitation

---

# Personal Reflection

Road strengthened my understanding of how web application vulnerabilities can serve as the entry point for a complete system compromise. The room reinforced the importance of methodical enumeration, careful analysis of application functionality, and structured Linux privilege escalation.
