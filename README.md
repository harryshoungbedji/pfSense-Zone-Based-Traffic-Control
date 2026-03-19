## pfSense-Zone-Based-Traffic-Control
Zone-based firewall implementation in pfSense with VirtualBox, showcasing network segmentation, access control policies, and secure traffic filtering across LAN and WLAN zones.


This is a hands-on virtual lab built in VirtualBox demonstrating zone-based firewall design using pfSense. The project implements permit and deny traffic policies across two network zones (LAN and WLAN), simulating a real-world corporate network segmentation scenario.

The lab is designed as a foundation that can be extended with additional security features such as IDS/IPS (Suricata), a DMZ zone for public-facing services, and AI-powered log analysis and automated incident response.

Note: The firewall rules applied in this lab are intentionally simplified for learning purposes. Some rules — such as allowing plain HTTP — would not be considered best practice in a production environment. These deliberate trade-offs are acknowledged and exist to demonstrate the contrast between permissive and restrictive policies. 

---

## Tools & Technologies Used

| Tool              | Version      | Purpose              |
|-------------------|--------------|----------------------|
|ViurtalBox         | 7.2.6        | Vitualization platform|
|pfSense            |Netgate 2.8.0 | Firewal / Router      |
|Kali Linux         | 2025.4       | LAN Client / Testing  |

# Network Rules Configuration Settings:

## Network Design  - Interfaces

| Interface            | Adapter                  | IP Address         |  Zone      |
|----------------------|--------------------------|-----------------|--------------|
|WAN (em0)             | NAT                      | 10.0.2.15/24 (DHCP) | Internet  |
|LAN (em1)             | Internal Network - LAN   | 192.168.1.1/24    | Trusted     |
|OPT1 (em2)            | Internal Network - WLAN  | 10.10.10.1/24     |Untrusted    |

## LAN Firewall Rules (Trusted Zone) [pfSense processes firewall rules
sequentially from top to bottom, stopping at the first rule that matches the traffic.]

| #    | Action        | Protocol       | Source      | Destination | Port | Purpose |
|-------|--------------|---------------|--------------|-------------|------|--------|
|1      | Allow        | Any           | Any          | LAN Address| 80  | Anti-Lockout Rule |
|2      | Allow        | ICMP          | LAN subnets  | Any        | -    | Ping /diagnostics |
|3      | Allow        | TCP           | LAN subnets  | Any        | 80   | HTTP web browsing |
|4      | Allow        | TCP           | LAN subnets  | Any        | 443  | HTTPS web browsing |
|5      | Allow        | UDP           | LAN subnets  | Any        | 53   | DNS resolution     |
|6      | Allow        | TCP           | LAN subnets  | Any        | 53   | DNS resolution(TCP)|
|7      | Block        | TCP           | LAN subnets  | Any        | 23   | Deny Telnet        |
|8      | Block        | TCP           | LAN subnets  | Any        | 23   | Deny FTP            |
|9      | Block        | Any           | LAN subnets  | Any        | Any  | Default Deny All    |

## WLAN Firewall Rules (Untrusted/Guest Zone)
1 | Block | Any | OPT1 subnets | LAN subnets | Any | Block WLAN to LAN
2 | Allow | UDP | OPT1 subnets | 10.10.10.1 | 53 | DNS to firewall only
3 | Allow | TCP | OPT1 subnets | Any | 443 | HTTPS only
4 | Block | TCP | OPT1 subnets | Any | 80 | Block HTTP
5 | Block | TCP | OPT1 subnets | Any | 22 | Block SSH
6 | Block | Any | OPT1 subnets | Any | Any | Default deny all





