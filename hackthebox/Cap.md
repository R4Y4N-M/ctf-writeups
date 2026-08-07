# Hack The Box Penetration Test Report

## Target Information

| Item | Details |
|------|----------|
| Machine | Cap |
| Platform | Hack The Box |
| IP Address | TARGET_IP |
| Difficulty | Easy |
| Test Type | Black Box |
| Tester | Rayan Massoud |
| Date | August 2026 |

---

# Executive Summary

A black-box penetration test was conducted against the Hack The Box "Cap" machine to identify security weaknesses that could lead to unauthorized access.

Three significant vulnerabilities were identified during the assessment. The most critical issue was the exposure of downloadable packet capture (PCAP) files containing plaintext FTP credentials. These credentials allowed SSH access to the target system. Further enumeration identified a Linux capability misconfiguration that resulted in full root compromise.

Overall Risk Rating: **High**

## Findings Summary

| Severity | Count |
|----------|------|
| Critical | 1 |
| High | 2 |
| Medium | 0 |
| Low | 0 |

---

# Scope

## In Scope

- Entire target machine
- All exposed network services

## Out of Scope

- Denial of Service attacks
- Brute-force attacks against unknown accounts
- External infrastructure

---

# Methodology

The assessment followed a five-phase penetration testing methodology.

## Phase 1 – Reconnaissance

Tools

- Nmap

Activities

- Port discovery
- Service detection
- Version enumeration

---

## Phase 2 – Enumeration

Tools

- Browser
- Gobuster
- Wireshark
- FTP

Activities

- Website analysis
- Directory enumeration
- Download and inspection of PCAP files
- Credential discovery

---

## Phase 3 – Exploitation

Recovered FTP credentials were successfully reused for SSH authentication, providing initial access to the target system.

---

## Phase 4 – Post Exploitation

Linux enumeration identified binaries with elevated capabilities.

Using Linux capabilities, privilege escalation to root was achieved.

---

# Findings

## Finding 001

### Exposed Packet Capture Files

Severity

**Critical**

CVSS

9.8

### Description

The application allowed unrestricted access to downloadable packet capture files.

One capture contained plaintext FTP credentials belonging to a valid local user.

### Impact

An attacker can recover valid credentials without authentication and reuse them across services.

### Evidence

- Downloaded PCAP file
- FTP authentication observed
- Credentials recovered

### Remediation

- Restrict access to PCAP files.
- Avoid storing sensitive traffic publicly.
- Encrypt authentication traffic whenever possible.

---

## Finding 002

### Password Reuse

Severity

High

CVSS

8.8

### Description

Recovered FTP credentials were also valid for SSH authentication.

### Impact

Password reuse allowed immediate compromise of the operating system.

### Evidence

Successful SSH login using recovered credentials.

### Remediation

- Enforce unique passwords.
- Deploy Multi-Factor Authentication.
- Monitor repeated credential usage.

---

## Finding 003

### Linux Capability Misconfiguration

Severity

High

CVSS

8.4

### Description

A binary possessed dangerous Linux capabilities that allowed privilege escalation.

### Impact

Complete system compromise.

### Evidence

Linux capability enumeration

```bash
getcap -r / 2>/dev/null
```

Root shell obtained.

### Remediation

- Remove unnecessary capabilities.
- Audit privileged binaries regularly.
- Apply system updates.

---

# Attack Chain

Reconnaissance

↓

Web Enumeration

↓

Download PCAP

↓

Recover FTP Credentials

↓

SSH Login

↓

Linux Enumeration

↓

Capability Abuse

↓

Root Access

---

# Remediation Summary

## Immediate

- Remove public PCAP access.
- Rotate exposed credentials.
- Remove dangerous capabilities.

## Short Term

- Implement password policy.
- Review Linux permissions.
- Audit exposed files.

## Long Term

- Perform regular penetration testing.
- Conduct configuration reviews.
- Implement centralized logging.

---

# Tools Used

| Tool | Purpose |
|------|----------|
| Nmap | Port Scanning |
| Gobuster | Directory Enumeration |
| Wireshark | PCAP Analysis |
| SSH | Remote Access |
| getcap | Capability Enumeration |

---

# Skills Demonstrated

- Network Enumeration
- Web Enumeration
- PCAP Analysis
- Credential Harvesting
- Linux Enumeration
- Privilege Escalation
- Technical Reporting

## Personal Reflection

Cap demonstrated how small misconfigurations can combine into a complete system compromise. I learned the importance of inspecting exposed files, analyzing packet captures for sensitive information, and auditing Linux capabilities during post-exploitation.
