# RootMe

## Machine Information

| Category | Details |
|----------|---------|
| Platform | TryHackMe |
| Difficulty | Easy |
| Type | Web Exploitation |

---

# Objective

Gain user access and escalate privileges to root.

---

# Tools Used

- Nmap
- Gobuster
- PHP Reverse Shell
- Netcat
- Linux Terminal

---

# Enumeration

## Nmap

```bash
nmap -sC -sV TARGET_IP
```

### Findings

- HTTP service
- SSH service

---

## Directory Enumeration

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Interesting directory discovered:

- /panel/

---

# Initial Access

The upload panel accepted a PHP payload after bypassing the upload restrictions.

A reverse shell was uploaded and executed.

Listener:

```bash
nc -lvnp 4444
```

---

# Privilege Escalation

System enumeration revealed files with the SUID bit set.

Useful commands:

```bash
find / -perm -4000 2>/dev/null
```

A vulnerable binary allowed privilege escalation to root.

---

# Lessons Learned

- File upload restrictions are not always effective.
- Always enumerate SUID binaries.
- GTFOBins is an important privilege escalation resource.

---

# Skills Practiced

- File Upload Exploitation
- Reverse Shells
- Linux Enumeration
- SUID Privilege Escalation

## Personal Reflection

RootMe helped me better understand file upload vulnerabilities and how weak validation mechanisms can be bypassed. I also gained valuable practice enumerating Linux systems and identifying SUID binaries that can be abused for privilege escalation.
