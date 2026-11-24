# Proxmox-Cybersecurity-Lab
  
Proxmox setup

### **1. Hardware**

- **CPU:** Ryzen 5 3600 6 cores 12 threads  
    
- **RAM:** 16GB DDR4 (2×8GB)  
    
- **GPU:** GTX 1660 Super (not currently passed through to VMs)  
    
- **Storage:** 500GB SSD  
    
- **Motherboard:** ASRock Fatal1ty B450 Gaming-ITX/ac  
    
- **PSU:** 600W Apevia

![Pasted image 20261120184112.png](app://4eb01deca2d0827ec1e6335dcef9b5ff45bd/D:/Cybersecurity/Cybersecurity/Proxmox%20Homelab/Pasted%20image%2020261120184112.png?1795218072446)

With some spare parts from upgrading my gaming PC, I built a mini PC node and installed Proxmox on it.

### **2. Proxmox Installation**

- Installed **Proxmox VE 9** on the 500GB SSD.  
    
- Assigned a static management IP:
    - **IP:** X.X.X.X  
        
    - **Subnet:** `/24` (`255.255.255.0`)  
        
    - **Gateway:** X.X.X.X  
        
- Configured the physical network interface through `vmbr0`.  
    
- Access Proxmox through your browser at:  
    [[https://X.X.X.X:8006](https://x.x.x.x:8006/)

20261120184436.png(app://4eb01deca2d0827ec1e6335dcef9b5ff45bd/D:/Cybersecurity/Cybersecurity/Proxmox%20Homelab/Pasted%20image%2020261120184436.png?1795218276253)

### **4. APT & Repository Configuration**

We fixed the package repository issues:

- Disabled the Proxmox Enterprise repositories that were returning `401 Unauthorized`.  
    
- Added the **Proxmox no-subscription repository** for Debian Trixie.  
    
- Fixed DNS temporarily using:
    - `1.1.1.1`  
        
    - `8.8.8.8`  
        
- Successfully ran `apt update`.  
    
- Reinstalled `proxmox-widget-toolkit` to restore the modified Proxmox UI files.

### **Virtual Machines**

**Kali Linux**

Attacker / testing VM

- 4 CPU cores  
    
- 4 GB RAM  
    
- XFCE desktop  
    

**Windows 11**

Target / testing VM

- Used for Windows labs  
    
- VirtIO drivers installed  
    
- Currently troubleshooting virtual display resolution  
    

### **6. Homelab Goals**

lab environment is intended for cybersecurity practice:

- **Kali Linux** — attacker machine  
    
- **Windows 11** — target machine  
    
- **Wazuh** — SIEM/log monitoring  
    
- **Pi-hole** — DNS/ad blocking  
    
- **Active Directory environment** — Windows Server domain controller and domain-joined Windows clients  
    
- **Isolated virtual networks** — for safely testing attacks without affecting your home network  
    

### **7. Remote Access**

I use **Tailscale** to access Proxmox remotely from your laptop without exposing Proxmox directly to the internet.
