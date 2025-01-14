---
{"dg-publish":true,"permalink":"/thm-notes/nmap/nmap-live-host-discovery/","title":"Live Host Discovery - NMAP","tags":["nmap","information-gathering"]}
---

# Nmap Scan Types and Commands

| Scan Type              | Example Command                             |
| ---------------------- | ------------------------------------------- |
| ARP Scan               | `sudo nmap -PR -sn MACHINE_IP/24`           |
| ICMP Echo Scan         | `sudo nmap -PE -sn MACHINE_IP/24`           |
| ICMP Timestamp Scan    | `sudo nmap -PP -sn MACHINE_IP/24`           |
| ICMP Address Mask Scan | `sudo nmap -PM -sn MACHINE_IP/24`           |
| TCP SYN Ping Scan      | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30`  |
| TCP ACK Ping Scan      | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30`  |
| UDP Ping Scan          | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |

*Remember to add `-sn` if you are only interested in host discovery without port-scanning. Omitting `-sn` will let Nmap default to port-scanning the live hosts.*

# Nmap Options and Their Purposes

| Option | Purpose                          |
|--------|----------------------------------|
| -n     | no DNS lookup                    |
| -R     | reverse-DNS lookup for all hosts |
| -sn    | host discovery only              |

[[THM Notes/NMAP/Nmap Post Scan Commands\|Nmap Post Scan Commands]]
[[THM Notes/NMAP/Nmap Advanced port scans\|Nmap Advanced port scans]]

-----
