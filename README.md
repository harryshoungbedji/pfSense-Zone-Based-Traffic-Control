## pfSense-Zone-Based-Traffic-Control
Zone-based firewall implementation in pfSense with VirtualBox, showcasing network segmentation, access control policies, and secure traffic filtering across LAN and WLAN zones.


---

## Tools & Technologies Used

| Tool              | Version      | Purpose              |
|-------------------|--------------|----------------------|
|ViurtalBox         | 7.2.6        | Vitualization platform|
|pfSense            |Netgate 2.8.0 | Firewal / Router      |
|Kali Linux         | 2025.4       | LAN Client / Testing  |


## Network Design  - Interfaces

| Interface            | Adapter                  | IP Address         |  Zone      |
|----------------------|--------------------------|-----------------|--------------|
|WAN (em0)             | NAT                      | 10.0.2.15/24 (DHCP) | Internet  |
|LAN (em1)             | Internal Network - LAN   | 192.168.1.1/24    | Trusted     |
|OPT1 (em2)            | Internal Network - WLAN  | 10.10.10.1/24     |Untrusted    |

## LAN Firewall Rules (Trusted Zone)

| #    | Action        | Protocol       | Source      | Destination | Port | Purpose |
|-------|--------------|---------------|--------------|-------------|------|--------|
|1      | Allow        | Any           | Any           | LAN Address| 80  | Anti-Lockout Rule |
|2      | Allow        | ICMP          | LAN subnets   | Any        | -    | Ping /diagnostics |
|3      | Allow        | TCP           | WLAN subnets  | Any        | 80   | HTTP web browsing |



