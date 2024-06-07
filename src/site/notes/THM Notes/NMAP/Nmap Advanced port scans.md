---
{"dg-publish":true,"permalink":"/thm-notes/nmap/nmap-advanced-port-scans/","title":"Nmap Advanced Port Scans","tags":["nmap","information-gathering"]}
---

# Nmap Port Scan Types and Commands

| Port Scan Type       | Example Command                                          |
|----------------------|-----------------------------------------------------------|
| TCP Null Scan        | `sudo nmap -sN 10.10.214.83`                              |
| TCP FIN Scan         | `sudo nmap -sF 10.10.214.83`                              |
| TCP Xmas Scan        | `sudo nmap -sX 10.10.214.83`                              |
| TCP Maimon Scan      | `sudo nmap -sM 10.10.214.83`                              |
| TCP ACK Scan         | `sudo nmap -sA 10.10.214.83`                              |
| TCP Window Scan      | `sudo nmap -sW 10.10.214.83`                              |
| Custom TCP Scan      | `sudo nmap --scanflags URGACKPSHRSTSYNFIN 10.10.214.83`   |
| Spoofed Source IP    | `sudo nmap -S SPOOFED_IP 10.10.214.83`                    |
| Spoofed MAC Address  | `sudo nmap --spoof-mac SPOOFED_MAC 10.10.214.83`          |
| Decoy Scan           | `nmap -D DECOY_IP,ME 10.10.214.83`                        |
| Idle (Zombie) Scan   | `sudo nmap -sI ZOMBIE_IP 10.10.214.83`                    |
| Fragment IP data into 8 bytes  | `sudo nmap -f 10.10.214.83`                     |
| Fragment IP data into 16 bytes | `sudo nmap -ff 10.10.214.83`                    |

*These scan types rely on setting TCP flags in unexpected ways to prompt ports for a reply. Null, FIN, and Xmas scans provoke a response from closed ports, while Maimon, ACK, and Window scans provoke a response from open and closed ports.*

# Nmap Options and Their Purposes

| Option               | Purpose                                      |
|----------------------|----------------------------------------------|
| --source-port PORT_NUM | specify source port number                  |
| --data-length NUM    | append random data to reach given length     |

| Option               | Purpose                                      |
|----------------------|----------------------------------------------|
| --reason             | explains how Nmap made its conclusion        |
| -v                   | verbose                                      |
| -vv                  | very verbose                                 |
| -d                   | debugging                                    |
| -dd                  | more details for debugging                   |
[[THM Notes/NMAP/Nmap Live Host Discovery\|Nmap Live Host Discovery]]
[[THM Notes/NMAP/Nmap Post Scan Commands\|Nmap Post Scan Commands]]


---------------------------
