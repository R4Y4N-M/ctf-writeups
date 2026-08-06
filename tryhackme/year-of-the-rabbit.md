# Year of the Rabbit

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Medium |
| Type | Web Exploitation |

---

# Objective

Gain initial access and successfully escalate privileges.

---

# Tools Used

- Nmap
- Gobuster
- Curl
- SSH
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

Identified hidden resources and useful files.

---

# Attack Path

Careful enumeration revealed the intended attack path.

Collected credentials and obtained access to the system.

---

# Post Exploitation

Performed Linux privilege escalation techniques.

Enumerated the system until a path to root was identified.

Useful commands:

```bash
sudo -l
find / -perm -4000 2>/dev/null
```

---

# Lessons Learned

- Patience during enumeration is critical.
- Small clues can reveal the intended attack path.
- Linux privilege escalation requires systematic enumeration.

---

# Skills Practiced

- Web Enumeration
- Linux Enumeration
- SSH
- Privilege Escalation

## Personal Reflection

Year of the Rabbit emphasized the importance of paying attention to small clues during enumeration. It reminded me that successful penetration testing is often a process of connecting multiple pieces of information together rather than finding one obvious vulnerability.
