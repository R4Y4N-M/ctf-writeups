# UltraTech

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Application Security, Docker, Linux Privilege Escalation |

---

# Objective

Compromise the target machine through web application enumeration, obtain an initial foothold, and escalate privileges to achieve full administrative access.

---

# Tools Used

- Nmap
- Gobuster
- Burp Suite Community
- Curl
- SSH
- Linux Terminal
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

Performed manual browsing together with directory enumeration.

Useful command:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration identified multiple web resources and an API endpoint that became the primary focus of the assessment.

---

# Attack Path

The engagement began with web application and API enumeration, which exposed functionality leading to valid credentials and initial access.

Following successful authentication, Linux enumeration identified privilege escalation opportunities that ultimately resulted in full administrative control of the target system.

---

# Post Exploitation

Performed Linux enumeration using standard techniques.

Useful commands included:

```bash
sudo -l
find / -perm -4000 2>/dev/null
getcap -r / 2>/dev/null
id
```

Enumeration revealed privilege escalation opportunities that were successfully leveraged to obtain root access.

---

# Lessons Learned

- API endpoints should always be included during web application enumeration.
- Docker environments require careful security configuration.
- Enumeration should continue after every successful privilege change.
- Small information disclosures can significantly simplify an attack path.

---

# Skills Practiced

- Web Enumeration
- API Enumeration
- Docker Enumeration
- Linux Enumeration
- Privilege Escalation
- Post Exploitation

---

# Personal Reflection

UltraTech expanded my understanding of web application assessments by introducing API enumeration and Docker-related security considerations. The room reinforced the importance of exploring every exposed service during reconnaissance and demonstrated how combining multiple enumeration techniques can lead to complete system compromise.
