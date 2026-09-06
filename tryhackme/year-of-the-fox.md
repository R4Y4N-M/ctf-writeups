# Year of the Fox

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Hard |
| Type | Web Application Security, Linux Privilege Escalation |

---

# Objective

Compromise the target machine by identifying weaknesses in the exposed services, obtaining an initial foothold, and escalating privileges to gain full administrative access.

---

# Tools Used

- Nmap
- Gobuster
- Burp Suite Community
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

Performed manual browsing together with directory enumeration to identify hidden resources and application functionality.

Useful command:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration revealed application functionality that contributed to obtaining initial access.

---

# Attack Path

The engagement began with web application enumeration and service analysis. Information gathered during reconnaissance enabled the discovery of valid credentials and the initial foothold.

Following successful authentication, Linux enumeration identified privilege escalation opportunities that ultimately resulted in root access.

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

Enumeration identified privilege escalation vectors that were successfully leveraged to obtain full administrative access.

---

# Lessons Learned

- Thorough enumeration remains the most important phase of a penetration test.
- Authentication weaknesses can quickly lead to complete system compromise.
- Linux privilege escalation requires continuous enumeration.
- Multiple small findings often combine into a successful attack path.

---

# Skills Practiced

- Web Enumeration
- Directory Enumeration
- Linux Enumeration
- SSH
- Privilege Escalation
- Post Exploitation

---

# Personal Reflection

Year of the Fox reinforced the value of maintaining a structured methodology throughout an engagement. Rather than depending on a single vulnerability, the room required careful reconnaissance, logical decision-making, and continuous Linux enumeration before privilege escalation became possible.
