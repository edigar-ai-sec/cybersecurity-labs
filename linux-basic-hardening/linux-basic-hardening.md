# Linux Basic Hardening Lab

**Repository**: cybersecurity-labs  
**Level**: Beginner / Blue Team  
**Focus**: Defensive Security & System Hardening

## Overview
This lab provides a practical checklist for basic Linux server hardening. All steps are defensive and aimed at reducing attack surface.

## Prerequisites
- A Linux VM (Ubuntu/Debian recommended)
- Root or sudo access

## Hardening Checklist

### 1. System Update
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install unattended-upgrades -y
```

### 2. User Management
```bash
# Create non-root user
sudo adduser secureuser

# Disable root SSH login
sudo sed -i 's/#PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config
```

### 3. SSH Hardening
```bash
sudo sed -i 's/#Port 22/Port 2222/' /etc/ssh/sshd_config
sudo sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config
sudo systemctl restart ssh
```

### 4. Firewall (UFW)
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2222/tcp
sudo ufw enable
```

### 5. Additional Hardening
- Install fail2ban: `sudo apt install fail2ban -y`
- Enable automatic security updates
- Disable unnecessary services
- Configure auditd for logging

## Verification Commands
```bash
sudo ufw status
ss -tuln
lastlog
```

## Next Steps
- Implement full CIS Benchmark
- Set up monitoring (OSSEC / Wazuh)

**Educational purpose only.** Always test in isolated environment.