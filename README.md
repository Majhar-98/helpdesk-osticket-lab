# 🎫 Help Desk Ticketing System — Home Lab Project
---

## 📌 Project Overview

This project involves the design, deployment, and configuration of a fully functional IT Help Desk ticketing system using **osTicket v1.18.1** on a virtualised **Ubuntu 26.04 LTS** server. The goal was to simulate a real enterprise IT support environment to develop practical skills relevant to Desktop Support and IT System Support roles.

---

## 🛠️ Technologies Used

| Component | Technology | Version |
|---|---|---|
| Virtualisation | Oracle VirtualBox | 7.x |
| Operating System | Ubuntu Server LTS | 26.04 (Resolute Raccoon) |
| Web Server | Apache2 | 2.4.x |
| Database | MySQL Server | 8.4.9 |
| Backend Language | PHP | 8.5.4 |
| Ticketing System | osTicket | 1.18.1 |
| Remote Access | OpenSSH Server | 1.10.2 |
| Network | VirtualBox NAT + Port Forwarding | — |

**Stack:** LAMP (Linux, Apache, MySQL, PHP)

---

## 🏗️ Architecture

```
Windows 11 Host PC
│
├── Oracle VirtualBox (Hypervisor)
│   └── Ubuntu 26.04 LTS VM (helpdesk)
│       ├── Apache2 Web Server (port 80)
│       ├── PHP 8.5
│       ├── MySQL 8.4 (osticket database)
│       └── osTicket v1.18.1
│
├── Port Forwarding Rules
│   ├── Host 8080 → Guest 80 (HTTP/Web)
│   └── Host 2222 → Guest 22 (SSH)
│
└── Windows Browser → http://127.0.0.1:8080/osticket/upload/scp
```

---

## ⚙️ Installation Steps

### 1. Environment Setup
- Installed Oracle VirtualBox on Windows 11
- Created Ubuntu 26.04 LTS VM with 2048 MB RAM, 25 GB disk
- Configured NAT network with port forwarding (SSH: 2222→22, HTTP: 8080→80)

### 2. Server Preparation
```bash
sudo apt update
sudo apt upgrade -y
```

### 3. Install Apache Web Server
```bash
sudo apt install apache2 -y
```

### 4. Install PHP and Required Extensions
```bash
sudo apt install php php-mysql php-xml php-intl php-apcu php-mbstring php-curl -y
```

### 5. Install MySQL Database Server
```bash
sudo apt install mysql-server -y
```

### 6. Download and Extract osTicket
```bash
wget https://github.com/osTicket/osTicket/releases/download/v1.18.1/osTicket-v1.18.1.zip
sudo apt install unzip -y
sudo unzip osTicket-v1.18.1.zip -d /var/www/html/osticket
```

### 7. Set File Permissions
```bash
sudo chown -R www-data:www-data /var/www/html/osticket
```

### 8. Configure MySQL Database
```sql
CREATE DATABASE osticket;
CREATE USER 'osticket'@'localhost' IDENTIFIED BY 'osticket123';
GRANT ALL PRIVILEGES ON osticket.* TO 'osticket'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 9. Configure osTicket
```bash
sudo cp /var/www/html/osticket/upload/include/ost-sampleconfig.php \
        /var/www/html/osticket/upload/include/ost-config.php
sudo chmod 0666 /var/www/html/osticket/upload/include/ost-config.php
```

### 10. Web Installer
- Opened browser at: `http://127.0.0.1:8080/osticket/upload/setup`
- Completed installation form with admin credentials and database details

### 11. Post-Installation Cleanup
```bash
sudo rm -rf /var/www/html/osticket/upload/setup
sudo chmod 0644 /var/www/html/osticket/upload/include/ost-config.php
```

---

## 🌐 Access URLs

| Portal | URL |
|---|---|
| User Ticket Portal | `http://127.0.0.1:8080/osticket/upload/` |
| Staff Control Panel | `http://127.0.0.1:8080/osticket/upload/scp` |
| Admin Panel | `http://127.0.0.1:8080/osticket/upload/scp` → Admin Panel |

---

## 🎯 Skills Demonstrated

- **Linux Server Administration** — Ubuntu Server setup, package management via APT, file permissions, service management with systemctl
- **Remote Server Management** — SSH configuration, key-based access, remote command execution via PowerShell
- **Network Configuration** — VirtualBox NAT setup, port forwarding rules for HTTP and SSH
- **LAMP Stack Deployment** — Full installation and configuration of Apache, MySQL, PHP on Linux
- **Database Administration** — MySQL database creation, user management, privilege assignment
- **IT Service Management** — Deployment of enterprise help desk software (osTicket), ticketing workflow configuration
- **Troubleshooting** — Resolved boot issues, password recovery, SSH connection problems, PHP extension conflicts

---

## 📋 Simulated IT Scenarios (Practice Tickets)

| Ticket # | Issue | Resolution |
|---|---|---|
| #001 | User cannot log into Windows | Password reset via admin |
| #002 | Printer not found on network | Driver reinstall + port configuration |
| #003 | Outlook not receiving emails | IMAP settings correction |
| #004 | Laptop running slow | Startup programs disabled, disk cleanup |
| #005 | New employee onboarding request | Account creation checklist followed |

---

## 📚 Resources Used

| Resource | Link |
|---|---|
| osTicket Official Documentation | https://docs.osticket.com |
| osTicket GitHub Releases | https://github.com/osTicket/osTicket/releases |
| Ubuntu Server Download | https://ubuntu.com/download/server |
| Oracle VirtualBox | https://www.virtualbox.org |
| Apache Documentation | https://httpd.apache.org/docs/ |
| MySQL Documentation | https://dev.mysql.com/doc/ |
| PHP Documentation | https://www.php.net/docs.php |

---

## 💡 Key Learnings

1. How enterprise help desk systems are deployed and managed
2. Linux server administration fundamentals
3. Network configuration and port forwarding in virtualised environments
4. LAMP stack architecture and component interaction
5. Remote server management via SSH
6. Database creation and user privilege management
7. Real-world troubleshooting methodology

---

## 🔮 Future Improvements

- [ ] Configure email integration for ticket notifications
- [ ] Set up multiple departments (IT Support, Hardware, Software)
- [ ] Create agent accounts and assign ticket queues
- [ ] Integrate with Active Directory (future AD home lab project)
- [ ] Add SSL/HTTPS using Let's Encrypt
- [ ] Automate VM snapshot backups

---

