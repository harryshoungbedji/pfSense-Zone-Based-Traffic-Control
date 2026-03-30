# Firewall Lab: WLAN vs LAN Segmentation

Virtual firewall lab built in VirtualBox using pfSense 2.8.1.
Implements firewall rules to allow trusted LAN access while
blocking untrusted WLAN from reaching internal resources.

## Objective
Build a virtual network environment to learn how to implement
firewall rules that control traffic between trusted and untrusted
networks. Trusted devices (LAN) get access to what they need.
Untrusted devices (WLAN) are denied access to anything on the
trusted side to defend against unwanted traffic and lateral movement.

## Tools Used
- VirtualBox 7.x
- pfSense 2.8.1
- Kali Linux
- Ubuntu Server 24.04

## Network Layout
| Zone | Interface | Subnet | Trust Level |
|---|---|---|---|
| WAN | em0 | NAT | Untrusted |
| LAN | em1 | 192.168.10.0/24 | Trusted |
| WLAN | em2 | 192.168.20.0/24 | Untrusted |

## Aligned With
- CompTIA CySA+ CS0-003
- NIST SP 800-41
- CIS Controls v8

## Validation Results
| Test | Expected | Result |
|---|---|---|
| WLAN internet access | Pass | ✅ Pass |
| WLAN → LAN host | Block | ✅ Blocked |
| WLAN → pfSense WebGUI | Block | ✅ Blocked |
| WLAN ping to LAN | Block | ✅ 100% loss |
| Nmap LAN from WLAN | Filtered | ✅ Filtered |

## Screenshots
See the screenshots/ folder for evidence of all tests.

## Full Documentation
See docs/firewall-lab
