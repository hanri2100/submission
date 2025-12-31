# Persamaan Perintah (Cheatsheet)

Perbandingan antara Debian-based (Ubuntu/Kali) vs RHEL-based (CentOS/RedHat).

1. INSTALL PACKAGE
   - Debian/Kali: `sudo apt install nmap`
   - RHEL/CentOS: `sudo dnf install nmap` (atau `yum`)

2. START SSH SERVICE
   - Debian/Kali: `sudo systemctl start ssh`
   - RHEL/CentOS: `sudo systemctl start sshd` (Perhatikan huruf 'd' di akhir)

3. CHECK SERVICE STATUS
   - Debian/Kali: `sudo systemctl status ssh`
   - RHEL/CentOS: `sudo systemctl status sshd`

4. ADD FIREWALL RULE (HTTP)
   - Debian/Kali: `sudo ufw allow 80/tcp`
   - RHEL/CentOS: `sudo firewall-cmd --add-port=80/tcp --permanent`

5. VIEW SYSTEM VERSION
   - Debian/Kali: `cat /etc/debian_version`
   - RHEL/CentOS: `cat /etc/redhat-release`
   - Universal:   `cat /etc/os-release`
