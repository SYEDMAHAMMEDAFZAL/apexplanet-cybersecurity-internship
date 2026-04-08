# 🔍 Task 2 — Network Security & Scanning
> **ApexPlanet Cybersecurity Internship | Days 13–24**

![Task](https://img.shields.io/badge/Task-2-blue)
![Track](https://img.shields.io/badge/Track-Network%20Security-teal)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

---

## 📌 Objective
Learn **reconnaissance, scanning, and network traffic analysis** using professional tools on a controlled lab environment.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| `nmap` | Port scanning & service detection |
| `whois` / `nslookup` | Passive reconnaissance |
| `OpenVAS` / `Nessus` | Vulnerability scanning |
| `Wireshark` | Packet capture & analysis |
| `hping3` | SYN flood simulation |
| `iptables` | Firewall rule creation |
| `netcat` | Banner grabbing |
| `Shodan` | Internet-facing asset search |

---

## 📋 Steps Completed

### 1. 🔍 Reconnaissance
#### Passive Recon
```bash
whois [target-domain]
nslookup [target-domain]
# Google Dorking: site:[target] filetype:pdf inurl:admin
shodan search [target-ip]
```

#### Active Recon
```bash
# Ping sweep — find live hosts
nmap -sn 192.168.x.0/24

# Banner grabbing
nc -v [target-ip] 80
```

---

### 2. 🔌 Port & Service Scanning
```bash
# TCP SYN Scan (stealth)
nmap -sS [target-ip]

# UDP Scan
nmap -sU [target-ip]

# Service version detection
nmap -sV [target-ip]

# OS detection
nmap -O [target-ip]

# Full aggressive scan (all in one)
nmap -A [target-ip]

# Save to file
nmap -A [target-ip] -oN nmap_scan_report.txt
```

**Key Open Ports Found on Metasploitable2:**
| Port | Service | Version |
|------|---------|---------|
| 21 | FTP | vsftpd 2.3.4 |
| 22 | SSH | OpenSSH 4.7p1 |
| 23 | Telnet | Linux telnetd |
| 80 | HTTP | Apache 2.2.8 |
| 139/445 | Samba | smbd 3.X |
| 3306 | MySQL | 5.0.51a |

---

### 3. 🚨 Vulnerability Scanning

#### Setup OpenVAS on Kali
```bash
sudo apt install openvas -y
sudo gvm-setup
sudo gvm-start
# Access at: https://127.0.0.1:9392
```

#### Key Vulnerabilities Found

| Vulnerability | Severity | CVE |
|--------------|----------|-----|
| vsftpd 2.3.4 Backdoor | 🔴 Critical | CVE-2011-2523 |
| Samba usermap_script | 🔴 Critical | CVE-2007-2447 |
| UnrealIRCd Backdoor | 🟠 High | CVE-2010-2075 |
| Telnet Plaintext | 🟠 High | — |
| Anonymous FTP Login | 🟡 Medium | — |
| PHP CGI Injection | 🟠 High | CVE-2012-1823 |

---

### 4. 🦈 Packet Analysis with Wireshark

#### Useful Wireshark Filters
```
http                          → HTTP traffic only
ftp                           → FTP commands (see credentials!)
dns                           → DNS queries
tcp.flags.syn == 1            → SYN packets (detect port scans)
ip.addr == [target-ip]        → Traffic to/from target
!(arp or dns or icmp)         → Remove noise
```

#### SYN Flood Simulation
```bash
# Simulate SYN flood (lab only!)
sudo hping3 -S --flood -p 80 [target-ip]

# Wireshark filter to see it:
tcp.flags.syn == 1 and tcp.flags.ack == 0
```

---

### 5. 🔥 Firewall with iptables
```bash
# View current rules
sudo iptables -L -v -n

# Allow SSH
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Block Telnet
sudo iptables -A INPUT -p tcp --dport 23 -j DROP

# Block NULL scan (port scan detection)
sudo iptables -A INPUT -p tcp --tcp-flags ALL NONE -j DROP

# Block XMAS scan
sudo iptables -A INPUT -p tcp --tcp-flags ALL ALL -j DROP

# Save rules
sudo iptables-save > /etc/iptables/rules.v4
```

---

## 📁 Repository Structure

```
task-2-network-security/
├── README.md                          ← This file
├── scan-notes.md                      ← Detailed scan analysis
├── Lab_Report_Task2_NetworkSecurity.docx
├── nmap_scan_report.txt               ← Raw Nmap output
└── screenshots/
    ├── passive-recon.png
    ├── nmap-full-scan.png
    ├── openvas-report.png
    ├── wireshark-ftp-creds.png
    ├── wireshark-syn-flood.png
    └── iptables-rules.png
```

---

## ✅ Deliverables

- [ ] Nmap Scan Report + OpenVAS Vulnerability Report
- [ ] GitHub Repo with detailed scan analysis ← *This repo*
- [ ] 5-min demo video showing scan & findings

---

## ⚠️ Disclaimer
> All scanning and exploitation techniques documented here were performed **only on intentionally vulnerable machines (Metasploitable2/DVWA) in a private, isolated lab network** for educational purposes. Never scan systems you do not own or have explicit permission to test.

---

*ApexPlanet Software Pvt. Ltd. | Cybersecurity Internship | SYEDMAHAMMEDAFZAL*
