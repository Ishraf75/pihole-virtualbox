Pi-hole DNS Ad-Blocking Server (Ubuntu Server on VirtualBox)

Overview
This project demonstrates how to deploy a Pi-hole DNS ad-blocking server on Ubuntu Server using VirtualBox.
The setup enables network-wide filtering for home devices, blocking ads and trackers at the DNS level.

Technologies Used
- Ubuntu Server 24.04 LTS
- Pi-hole
- VirtualBox (Bridged Networking)
- UFW Firewall
- macOS Host
- iPhone / Personal Devices (Client Testing)

Setup Steps

1. Create Virtual Machine
- OS: Ubuntu Server
- RAM: 2 GB
- Storage: 50 GB
- Network: Bridged Adapter
- Enable SSH during installation

2. Install Pi-hole
    curl -sSL https://install.pi-hole.net | bash
- Select OpenDNS or Cloudflare as the upstream provider
- Enable the web interface
- Note the password provided at the end of installation

3. Configure Firewall (UFW)
    sudo ufw allow OpenSSH
    sudo ufw allow 53/tcp
    sudo ufw allow 53/udp
    sudo ufw allow 80/tcp
    sudo ufw enable
    sudo ufw status

4. Set Static IP
- Use 'ip a' to identify the interface name (e.g., enp0s8)
- Update /etc/netplan/*.yaml to assign a static IP
- Apply configuration:
    sudo netplan apply

5. Access Dashboard
- Visit http://192.168.1.88/admin
- Log in using the Pi-hole password

6. Test DNS Filtering
    nslookup doubleclick.net 192.168.1.88
Expected output → 0.0.0.0 (blocked)

Verification
- Confirmed DNS blocking through Pi-hole dashboard query logs
- Verified access from multiple client devices (MacBook, iPhone)
- Monitored DNS traffic and blocking rates in real time

Summary
Built and configured a Pi-hole DNS server on Ubuntu (VirtualBox) providing network-wide filtering across home devices.
Implemented bridged networking, static IP, and UFW firewall rules; verified operation through DNS testing and dashboard logs.
