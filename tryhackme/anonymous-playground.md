# Anonymous Playground

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Hard |
| Type | Binary Exploitation, Linux Privilege Escalation |

---

# Objective

Compromise the target machine by performing thorough reconnaissance, identifying weaknesses in the exposed services, obtaining an initial foothold, and escalating privileges through multiple stages until full administrative access is achieved.

---

# Tools Used

- Nmap
- Gobuster
- Python
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

- SSH
- HTTP

## Web Enumeration

Performed manual browsing and directory enumeration to identify application resources and gather information useful for the initial attack.

Useful command:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Enumeration revealed information that contributed to obtaining an initial foothold.

---

# Attack Path

The engagement began with web application and service enumeration before transitioning into binary analysis and exploitation techniques.

Following initial access, multiple privilege boundaries required continuous Linux enumeration and exploitation before root access was achieved.

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

Multiple privilege escalation stages ultimately resulted in root access.

---

# Lessons Learned

- Enumeration remains the foundation of every successful assessment.
- Binary exploitation requires careful analysis rather than guesswork.
- Linux privilege escalation should be repeated after every privilege change.
- Chaining multiple techniques together is often necessary on harder machines.

---

# Skills Practiced

- Web Enumeration
- Binary Analysis
- Linux Enumeration
- Privilege Escalation
- Post Exploitation

---

# Personal Reflection

Anonymous Playground was one of the most technically challenging rooms I have completed so far. It required patience, structured problem-solving, and adapting to several different exploitation techniques throughout the engagement. Completing this room significantly improved my confidence with binary exploitation concepts while reinforcing the importance of disciplined Linux enumeration and privilege escalation.
