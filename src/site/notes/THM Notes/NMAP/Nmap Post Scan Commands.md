---
{"title":"Nmap Post Port Scans","date":"2024-05-18 16:37:59","tags":["nmap","information-gathering"],"categories":["cybersecurity","THM","NMAP"],"feature":false,"cover":"https://techyrick.com/wp-content/uploads/2021/09/nmap.webp","dg-publish":true,"walkthrough":"https://blog.satvik.live/post/THM%2FNMAP%2FNmap-Post-Port-Scans","roomlink":"https://tryhackme.com/r/room/nmap04","permalink":"/thm-notes/nmap/nmap-post-scan-commands/","dgPassFrontmatter":true}
---

# Nmap Options and Their Meanings

| Option                  | Meaning                                         |
| ----------------------- | ----------------------------------------------- |
| -sV                     | determine service/version info on open ports    |
| -sV --version-light     | try the most likely probes (2)                  |
| -sV --version-all       | try all available probes (9)                    |
| -O                      | detect OS                                       |
| --traceroute            | run traceroute to target                        |
| --script=SCRIPTS        | Nmap scripts to run                             |
| -sC or --script=default | run default scripts                             |
| -A                      | equivalent to -sV -O -sC --traceroute           |
| -oN                     | save output in normal format                    |
| -oG                     | save output in grepable format                  |
| -oX                     | save output in XML format                       |
| -oA                     | save output in normal, XML and Grepable formats |
|                         |                                                 |

[[THM Notes/NMAP/Nmap Advanced port scans\|Nmap Advanced port scans]]
[[THM Notes/NMAP/Nmap Live Host Discovery\|Nmap Live Host Discovery]]

----
