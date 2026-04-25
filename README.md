# Home Lab doc 1.0
> A personal IT lab built to develop hands-on skills in virtualization,
> networking, and systems administration.

---

## 📋 Overview
This homelab runs on a repurposed thin client using VMware vSphere as the
hypervisor. It primarily serves as a personal learning environment for practising
enterprise-level IT concepts including networking/firewalling, VPN configuration,
and virtual machine management. In the future, I also aim to utilize this to provide
additional services for myself, friends, and peers. This may include storage solutions,
server hosting, etc. and is an ongoing work in progress.

## Tech Stack
| Component        | Technology           | Purpose                          |
|------------------|----------------------|----------------------------------|
| Hypervisor       | VMware vSphere       | Host for all virtual machines    |
| Firewall/Router  | OPNsense             | Network security & routing       |
| VPN Server       | Ubuntu Server 22.04  | Remote access via OpenConnect    |
| Smart Home       | HAOS                 | Unification of smart devices     |
| Test Environment | Virtual Desktops     | Software & config testing        |

Technology and network stack brief overview:
- Hypervisor is connected to both incoming ISP WAN traffic and outgoing LAN
- Hypervisor hosts OPNsense as primary router and firewall for LAN
- VLANs segment traffic between production, testing, and management zones
- Ubuntu Server provides VPN tunnel for secure remote access


## 🌐 Network Topology
<!-- Add your diagram image here once created in draw.io -->
<!-- ![Network Diagram](diagrams/network-topology.png) -->

## 📁 Repository Structure
```
homelab/
├── [README.md](README.md)                        ← You are here
├── network/
│   └── [opnsense-setup.md](network/opnsense-setup.md)   ← Firewall rules, VLANs, DNS config
├── servers/
│   └── [ubuntu-vpn.md](servers/ubuntu-vpn.md)           ← VPN server setup walkthrough
├── virtualization/
│   └── [vsphere-overview.md](virtualization/vsphere-overview.md) ← VM inventory and vSphere config
└── diagrams/
    └── network-topology.png
```

## ✅ Skills Demonstrated
- Hypervisor setup and virtual machine provisioning (VMware vSphere)
- Physical and virtual network adapter configuration for WAN/LAN separation
- Firewall configuration, routing, and DHCP management (OPNsense)
- Linux server administration (Ubuntu Server 22.04)
- VPN deployment using OpenConnect over TCP 443 with SSL/TLS certificates (Let's Encrypt)
- Cloud VPS provisioning and configuration (Linode)
- Network traffic obfuscation and deep packet inspection evasion
- Smart home automation and device integration (Home Assistant OS)
- Documentation and technical writing

## 🔭 In Progress / Future Plans
- [ ] Set up a SIEM (e.g. Wazuh or Splunk) for log monitoring
- [ ] Configure automated backups for VMs
- [ ] Deploy VLANs for an IoT test environment and network segmentation
- [ ] Add IDS/IPS rules to OPNsense
- [ ] Set up a NAS

## 🧠 Lessons Learned
- VMware vSphere NIC configuration: Configured two network adapters in vSphere — an onboard NIC for LAN and a USB NIC adapter for WAN — and assigned -  them as virtual interfaces for OPNsense to handle routing and firewall duties.
- OPNsense startup/connectivity issue: After rebooting vSphere, OPNsense was not set to auto-start, leaving the network without DHCP. My PC received an APIPA address and lost access to the management subnet. Resolved by manually setting a static IP on my PC to match the correct subnet and reconnecting to vSphere, then correcting OPNsense's startup behavior.
- OpenConnect VPN — Home Lab: Deployed an OpenConnect VPN server on Ubuntu Server 22.04, configured to run on TCP 443 to disguise traffic as HTTPS and bypass deep packet inspection. Obtained a trusted SSL certificate via Let's Encrypt/Certbot. Port forwarding was configured on OPNsense to route inbound traffic to the VPN server.
- OpenConnect VPN — Cloud VPS (Linode): Provisioned and configured a separate Ubuntu Server instance on a Linode VPS with the same OpenConnect setup, specifically to bypass the Great Firewall of China and maintain secure remote access while overseas.
- LAN design and DHCP: Configured OPNsense as the DHCP server for my preferred subnet with a defined lease range, and assigned OPNsense itself a static IP. All VMs and devices sit on this subnet.

---
*Built and maintained by Edward Pan | LinkedIn: linkedin.com/in/edwardxpan/ | Last updated: April 2026*
