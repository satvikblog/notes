---
{"dg-publish":true,"permalink":"/thm-notes/nmap/nmap-post-scan-commands/","title":"Nmap Post Port Scans","tags":["nmap","information-gathering"]}
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
