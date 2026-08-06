# Pickle Rick

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Easy |
| Type | Web Exploitation |
| Skills Practiced | Enumeration, Web Exploitation, Reverse Shell, Linux Privilege Escalation |

---

# Objective

Gain initial access to the target machine and escalate privileges to obtain root access.

---

# Tools Used

- Nmap
- Gobuster
- PHP Reverse Shell
- Netcat
- Linux Terminal

---

# Enumeration

## Nmap Scan

```bash
nmap -sC -sV TARGET_IP
```

### Findings

- HTTP service running
- Apache Web Server
- Website accessible through port 80

---

## Directory Enumeration

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Interesting directories discovered:

- login.php
- assets/
- robots.txt

---

## robots.txt

Checking `robots.txt` revealed useful information that helped during the attack.

---

# Initial Access

After discovering the login page, I enumerated the website and gathered enough information to authenticate.

Once logged in, I explored the available functionality and located a page that allowed command execution.

---

# Reverse Shell

A PHP reverse shell was uploaded to obtain a fully interactive shell.

Example listener:

```bash
nc -lvnp 4444
```

After triggering the payload, a shell was obtained on the target machine.

---

# Privilege Escalation

After gaining access, I enumerated the system.

Useful commands included:

```bash
sudo -l
whoami
id
hostname
```

I discovered the current user had sudo privileges that allowed privilege escalation.

Root access was obtained using the allowed sudo command.

---

# Lessons Learned

- Enumeration is the most important phase.
- Always inspect robots.txt.
- Directory brute forcing often reveals hidden functionality.
- Understanding Linux permissions is essential for privilege escalation.
- Always check sudo permissions immediately after gaining a shell.

---

# Skills Practiced

- Web Enumeration
- Directory Brute Forcing
- Linux Enumeration
- Reverse Shells
- Privilege Escalation

## Personal Reflection

This room reinforced the importance of thorough enumeration. It also gave me more practice working with Linux privilege escalation techniques.
