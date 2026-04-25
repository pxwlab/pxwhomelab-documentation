---

## Interface Assignment

OPNsense was configured with two VMware virtual NICs:

- **vmx0 — LAN:** Mapped to the onboard NIC, serving all internal devices
- **vmx1 — WAN:** Mapped to a USB NIC adapter, receiving and sending internet traffic

Interface assignment was completed via the OPNsense console on first boot,
which required correctly identifying and mapping each physical adapter to its
respective role. Incorrect initial assignment caused routing issues that were
resolved by reassigning interfaces through the console menu.

---

## DHCP Configuration

DHCP is handled entirely by OPNsense for the 10.10.10.0/24 subnet.

**Static IP Assignments:**

| Device | IP Address |
|---|---|
| OPNsense (WebGUI) | 10.10.10.1 |
| TP-Link AP | 10.10.10.2 |
| Hue Bridge | 10.10.10.5 |
| vSphere Host | 10.10.10.10 |
| PC | 10.10.10.20 |
| Ubuntu Server | 10.10.10.183 |

> All VMs and physical devices sit on this subnet. VLAN segmentation is planned
> for a future iteration.

---

## DNS Configuration

- **DNS Server:** 1.1.1.1 (Cloudflare)
- **Gateway:** None (resolved directly by OPNsense)
- Configured under `System → Settings → General`

Cloudflare's 1.1.1.1 was chosen for reliability and privacy over default ISP DNS.

---

## Firewall Rules

- Default LAN-to-WAN traffic is permitted
- **Bogon networks blocking** is enabled on the WAN interface, preventing traffic
  from invalid or unallocated IP ranges
- Port forwarding rule configured for OpenConnect VPN (TCP 443)

### Port Forward — OpenConnect VPN

| Field | Value |
|---|---|
| Protocol | TCP |
| WAN Port | 443 |
| Destination | 10.10.10.183 (Ubuntu Server) |
| Purpose | Route inbound VPN traffic to Ubuntu VPN server |

> **Troubleshooting note:** After configuring the port forward rule, an associated
> firewall PASS rule must be enabled to allow the traffic through. Initially this
> rule was not activated, resulting in failed VPN connections and loss of internet
> access after connecting. Enabling the PASS rule resolved the issue.

---

## Wireless Access Point — TP-Link (AP Mode)

The TP-Link router is configured in **Access Point mode**, meaning:

- DHCP is disabled on the TP-Link itself
- It connects back to the physical switch, which feeds into vSphere/OPNsense
- All IP assignment and routing is handled by OPNsense
- Wireless clients receive 10.10.10.x addresses just like wired devices

---

## Lessons Learned

- Incorrect WAN/LAN interface assignment on first boot caused a routing loop.
  Resolved via the OPNsense console by reassigning vmx0 and vmx1 correctly.
- After rebooting vSphere, OPNsense was not set to auto-start. With no DHCP
  available, connected devices received APIPA addresses. Fixed by enabling
  OPNsense auto-start in vSphere and manually setting a static IP on the PC
  to regain management access.
- Port forward PASS rule must be explicitly enabled alongside the forwarding
  rule — the port forward alone does not permit traffic through the firewall.

---

*Part of the [pxwhomelab-documentation](../../README.md) |  Last updated: March 2026*
