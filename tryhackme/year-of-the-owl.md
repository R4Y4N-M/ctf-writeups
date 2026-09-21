# TryHackMe – Year of the Owl

 Difficulty: Medium
 Platform: TryHackMe
 Category: Web Exploitation / Linux Privilege Escalation

# Objective

The goal of this room was to gain initial access to the target machine through web enumeration and exploitation, then perform privilege escalation to obtain the root flag.

# Skills Practiced:
- SMB Enumeration
- Credential Discovery
- Remote PowerShell Administration (WinRM)
- Windows Enumeration
- Privilege Escalation Methodology
- Post-Exploitation
- Documentation

  
# Tools Used
- Nmap
- Gobuster
- Evil-WinRM
- SMBClient
- PowerShell
- WinPEAS


# Methodology

# 1. Initial Enumeration

The first step was identifying open ports and running services.

Example:

nmap -sC -sV -oN nmap.txt <TARGET_IP>

Information gathered included:

- Open TCP ports
- Web service
- SSH service
- Service versions

This established the attack surface.

# 2. Web Enumeration

The website contained limited information, so directory brute forcing was performed.

Example:

gobuster dir \
-u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

Interesting directories and files were discovered.

These hidden resources became the primary attack path.

# 3. Information Gathering

Further inspection revealed useful information such as:

- Hidden pages
- Credentials
- Source code comments
- Configuration files
- Usernames

Each discovery helped build the attack chain.

# 4. Initial Access

After identifying the exposed services during enumeration, I investigated the available SMB shares to gather additional information. 
The SMB enumeration revealed files and data that assisted in identifying valid credentials and understanding the target environment. 
Once valid credentials were obtained, I authenticated to the Windows host using Evil-WinRM, which provided a PowerShell session for further post-exploitation activities.

Once inside, user enumeration was performed.

Example:

whoami
hostname
id
pwd

# 5. Local Enumeration

After gaining remote access through Evil-WinRM, I performed standard Windows enumeration to identify privilege escalation opportunities.
This included reviewing user privileges, installed software, scheduled tasks, services, and configuration files to better understand the security posture of the host.


# 6. Privilege Escalation

The intended privilege escalation path was identified after local enumeration.

This involved abusing a system misconfiguration to gain elevated privileges.

Once successful:

id

returned

uid=0(root)

confirming root access.

# 7. Capture Flags

Finally:

cat user.txt

and

cat root.txt

were used to retrieve both flags.

# Lessons Learned

This room reinforced several important penetration testing concepts:

- Never rely solely on visible web content.
- Directory brute forcing often reveals hidden attack paths.
- Thorough Linux enumeration is essential.
- Privilege escalation depends on identifying small misconfigurations.
- Enumeration is usually more important than exploitation.


# Commands Used
nmap -sC -sV TARGET_IP

gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

ssh user@TARGET_IP

sudo -l

find / -perm -4000 2>/dev/null

id

whoami

hostname


# MITRE ATT&CK Mapping

| Technique | MITRE ID |
|-----------|-----------|
| Active Scanning | T1595 |
| Network Service Discovery | T1046 |
| Gather Victim Network Information | T1590 |
| Exploit Public Facing Application | T1190 |
| Valid Accounts | T1078 |
| Command and Scripting Interpreter | T1059 |
| File and Directory Discovery | T1083 |
| Permission Groups Discovery | T1069 |
| Privilege Escalation | T1068 |


# Reflection

Year of the Owl emphasized the importance of structured enumeration before attempting exploitation. By systematically identifying exposed services, hidden web content, and system misconfigurations, I was able to gain an initial foothold and successfully escalate privileges. The room reinforced that effective penetration testing is driven by careful information gathering and methodical analysis rather than rushing into exploits. It also strengthened my confidence with Linux enumeration, privilege escalation techniques, and maintaining a logical attack workflow suitable for real-world assessments.
