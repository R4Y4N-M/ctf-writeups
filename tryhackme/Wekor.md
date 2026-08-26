# Wekor

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Application Security, Linux Privilege Escalation |

---

# Objective

Compromise the target machine by identifying weaknesses in the web application, obtaining an initial foothold, and escalating privileges to gain full administrative access.

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

- HTTP
- SSH

## Web Enumeration

Performed manual browsing and directory enumeration to identify application functionality and hidden resources.

Useful command:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration revealed application components that became the primary attack surface.

---

# Attack Path

The assessment began with web application enumeration, leading to the discovery of weaknesses that allowed initial access to the target system.

After obtaining a user shell, Linux enumeration identified privilege escalation opportunities that resulted in full administrative access.

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

Enumeration identified privilege escalation vectors that ultimately resulted in root access.

---

# Lessons Learned

- Web application functionality should be thoroughly reviewed during reconnaissance.
- Enumeration should continue after every successful privilege escalation step.
- Linux privilege escalation depends on understanding permissions and system configuration.
- Small web application weaknesses can lead to complete operating system compromise.

---

# Skills Practiced

- Web Enumeration
- Burp Suite
- Linux Enumeration
- Privilege Escalation
- Post Exploitation

---

# Personal Reflection

Wekor strengthened my understanding of how web application vulnerabilities can serve as the starting point for a full system compromise. The room reinforced the importance of methodical enumeration, careful analysis of application functionality, and systematic Linux privilege escalation.
