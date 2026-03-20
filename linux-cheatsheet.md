# 🐧 Linux Command Cheat-Sheet
> **ApexPlanet Cybersecurity Internship — Task 1**

---

## 📂 File System Navigation

| Command | Description | Example |
|---------|-------------|---------|
| `pwd` | Print working directory | `pwd` → `/home/kali` |
| `ls` | List files | `ls -la` (detailed + hidden) |
| `cd` | Change directory | `cd /var/log` |
| `mkdir` | Create directory | `mkdir mydir` |
| `rm` | Remove file/dir | `rm -rf mydir` ⚠️ |
| `cp` | Copy | `cp file.txt /tmp/` |
| `mv` | Move/rename | `mv old.txt new.txt` |
| `find` | Search files | `find / -name "*.log"` |
| `cat` | Read file | `cat /etc/passwd` |
| `less` | Paginate file | `less bigfile.txt` |

---

## 🔐 File Permissions

```
-rwxr-xr--  1  owner  group  size  date  filename
 ↑↑↑ ↑↑↑ ↑↑↑
 │   │   └── Others: r-- = read only
 │   └────── Group:  r-x = read + execute
 └────────── Owner:  rwx = full access
```

| Command | Description | Example |
|---------|-------------|---------|
| `chmod` | Change permissions | `chmod 755 script.sh` |
| `chown` | Change owner | `chown root:root file.txt` |
| `ls -l` | View permissions | `ls -l /etc/shadow` |

**Permission Numbers:**
| # | Permission |
|---|-----------|
| 7 | rwx (full) |
| 6 | rw- (read+write) |
| 5 | r-x (read+exec) |
| 4 | r-- (read only) |
| 0 | --- (none) |

---

## 📦 Package Management (Debian/Kali)

| Command | Description |
|---------|-------------|
| `apt update` | Update package list |
| `apt upgrade` | Upgrade installed packages |
| `apt install <pkg>` | Install a package |
| `apt remove <pkg>` | Remove a package |
| `apt search <name>` | Search for package |
| `dpkg -i file.deb` | Install .deb manually |
| `dpkg -l` | List installed packages |
| `dpkg -L <pkg>` | List files in package |

---

## 🌐 Networking Commands

| Command | Description | Example |
|---------|-------------|---------|
| `ifconfig` | View network interfaces | `ifconfig eth0` |
| `ip a` | Modern ifconfig | `ip addr show` |
| `ip r` | Show routing table | `ip route` |
| `ping` | Test connectivity | `ping 192.168.1.1 -c 4` |
| `netstat -an` | View all connections | `netstat -tuln` |
| `ss -tuln` | Modern netstat | `ss -tuln` |
| `traceroute` | Trace route to host | `traceroute google.com` |
| `nslookup` | DNS lookup | `nslookup google.com` |
| `dig` | Advanced DNS query | `dig google.com` |
| `whois` | Domain info | `whois example.com` |
| `wget` | Download file | `wget http://url/file` |
| `curl` | HTTP request | `curl -I http://target` |

---

## 🔍 Nmap Quick Reference

```bash
# Basic scan
nmap 192.168.1.1

# Scan a subnet
nmap 192.168.1.0/24

# Version detection
nmap -sV 192.168.1.1

# OS detection
nmap -O 192.168.1.1

# Full aggressive scan
nmap -A 192.168.1.1

# Scan specific ports
nmap -p 22,80,443 192.168.1.1

# Save output
nmap -sV 192.168.1.1 -oN scan_results.txt
```

---

## 🦈 Wireshark Filters

| Filter | Description |
|--------|-------------|
| `ip.addr == 192.168.1.1` | Traffic to/from IP |
| `tcp.port == 80` | HTTP traffic |
| `icmp` | Ping packets only |
| `http` | HTTP traffic |
| `dns` | DNS queries |
| `tcp.flags.syn == 1` | TCP SYN packets |
| `!(arp or dns)` | Exclude noise |

---

## 🔒 OpenSSL Commands

```bash
# Encrypt a file
openssl enc -aes-256-cbc -in plain.txt -out encrypted.bin

# Decrypt a file
openssl enc -d -aes-256-cbc -in encrypted.bin -out decrypted.txt

# Generate MD5 hash
md5sum filename.txt

# Generate SHA256 hash
sha256sum filename.txt

# View certificate details
openssl x509 -in cert.pem -text -noout
```

---

## 🛠️ Useful System Commands

| Command | Description |
|---------|-------------|
| `whoami` | Current user |
| `id` | User ID + groups |
| `uname -a` | System info |
| `ps aux` | Running processes |
| `top` / `htop` | Process monitor |
| `df -h` | Disk space |
| `free -h` | Memory usage |
| `history` | Command history |
| `sudo su` | Switch to root |
| `passwd` | Change password |

---

## ⌨️ Bash Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + C` | Kill current process |
| `Ctrl + Z` | Suspend process |
| `Ctrl + L` | Clear terminal |
| `Ctrl + R` | Search command history |
| `Tab` | Autocomplete |
| `!!` | Repeat last command |
| `!n` | Run command #n from history |

---

*ApexPlanet Software Pvt. Ltd. | Cybersecurity Internship — Task 1*
