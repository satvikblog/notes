---
{"title":"Live Host Discovery - NMAP","date":"2024-05-16 19:29:01","tags":["nmap","information-gathering"],"categories":["cybersecurity","THM","NMAP"],"cover":"https://techyrick.com/wp-content/uploads/2021/09/nmap.webp","feature":false,"dg-publish":true,"roomlink":"https://tryhackme.com/r/room/nmap01","walkthrough":"https://blog.satvik.live/post/THM%2FNMAP%2FLive-Host-Discovery","permalink":"/thm-notes/nmap/nmap-live-host-discovery/","dgPassFrontmatter":true}
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
