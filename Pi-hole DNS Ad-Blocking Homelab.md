## Project Overview

Deployed Pi-hole on my Proxmox homelab to provide network-level DNS filtering and block advertisements, trackers, and unwanted domains. This project allowed me to practice Linux administration, DNS configuration, virtualization, and network troubleshooting.



![[Pasted image 20261123215249.png]]

## Environment

- **Hypervisor:** Proxmox VE
    
- **Deployment:** LXC container
    
- **Operating System:** Debian 13
    
- **Container type:** Unprivileged
    
- **CPU:** 1 vCPU
    
- **Memory:** 512 MB
    
- **Storage:** 8 GB
    
- **Network:** `vmbr0` bridge
    
- **IP configuration:** Static IP address
    
- **Upstream DNS:** Cloudflare (`1.1.1.1` and `1.0.0.1`)
    

## Installation

Updated the Debian system and installed the required dependencies:

```bash
apt update
apt upgrade -y
apt install curl -y
```

Installed Pi-hole using its official installation script:

```bash
curl -sSL https://install.pi-hole.net | bash
```

During installation, configured the following:

- Selected the network interface.
    
- Configured the upstream DNS provider to Cloudflare.
    
- Enabled query logging.
    
- Set privacy mode to **Show Everything** for lab monitoring.
    

## Configuration

### Web Administration

Accessed the Pi-hole administrative dashboard through its web interface:

```text
http://PIHOLE-IP/admin
```

Set the administrator password using:

```bash
pihole setpassword
```

### Windows Client DNS Configuration

Configured my Windows PC to use Pi-hole as its DNS server by manually setting the preferred DNS server to Pi-hole's IP address and leaving the alternate DNS server blank.

This allows DNS requests from my PC to pass through Pi-hole for filtering.

## Testing and Validation

### DNS Resolution Test

Used `nslookup` to verify DNS resolution through Pi-hole:

```bash
nslookup google.com PIHOLE-IP
```

Confirmed that DNS resolution was working and that my PC appeared in Pi-hole's Query Log.

### Domain Blocking Test

Added a test domain manually through Pi-hole's Domain Management:

- Type: Exact deny
    
- Status: Enabled
    
- Group: Default
    

Tested the domain using `nslookup` and confirmed Pi-hole returned `0.0.0.0`, verifying that the domain-blocking rule was functioning.

## Blocklists

Pi-hole uses blocklists to prevent DNS resolution for known advertising, tracking, and unwanted domains.

The default StevenBlack hosts list was successfully loaded during the Gravity update.

Additional blocklists can be added through the Adlists section of the dashboard. After adding or modifying lists, Gravity must be updated to download and process the blocklist data.

## Technologies and Skills Practiced

- Linux system administration
    
- Debian package management
    
- Proxmox virtualization and LXC containers
    
- DNS configuration and troubleshooting
    
- Network client configuration
    
- DNS filtering and domain blocking
    
- Command-line troubleshooting
    
- Log monitoring and validation
    
- Infrastructure deployment
    

## Future Improvements

- Add and test additional reputable DNS blocklists.
    
- Configure remote access through Tailscale.
    
- Explore subnet routing to access Pi-hole remotely without exposing services to the public internet.
    
- Document DNS queries and troubleshooting scenarios.
    
- Explore integration with additional homelab security monitoring tools.