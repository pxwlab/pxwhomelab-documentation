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
├── README.md               ← You are here
├── network/
│   └── opnsense-setup.md   ← Firewall rules, VLANs, DNS config
├── servers/
│   └── ubuntu-vpn.md       ← VPN server setup walkthrough
├── virtualization/
│   └── vsphere-overview.md ← VM inventory and vSphere config
└── diagrams/
    └── network-topology.png
```

## ✅ Skills Demonstrated
- Hypervisor setup and virtual machine provisioning (VMware vSphere)
- Firewall configuration and network segmentation (OPNsense)
- Linux server administration (Ubuntu Server 22.04)
- VPN deployment and remote access configuration
- Documentation and technical writing

## 🔭 In Progress / Future Plans
- [ ] Set up a SIEM (e.g. Wazuh or Splunk) for log monitoring
- [ ] Configure automated backups for VMs
- [ ] Deploy a VLAN for an IoT test environment
- [ ] Add IDS/IPS rules to OPNsense

## 🧠 Lessons Learned
- **OPNsense initial config:** Ran into a routing loop during first setup.
  Resolved by correcting the WAN/LAN interface assignments in the console.
- **VPN split tunneling:** Configured split-tunnel so only lab traffic
  routes through VPN, keeping personal browsing separate.

---
*Built and maintained by [Your Name] | Last updated: [Month Year]*
