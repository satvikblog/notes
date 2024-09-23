---
{"dg-publish":true,"permalink":"/footprinting-and-scanning/","title":"Footprinting & Scanning","tags":["nmap","ejptv2","information-gathering"]}
---

**Basic Host Discovery using ping scan**
```bash
nmap -sn <target_IP>
```
**Basic Port Scan**
```bash
nmap -sS -T4 -p- <target_IP>
```
**Service Version Detection**
```bash
nmap -sS -sV -p- -T4 <target_IP>
```
**OS Detection along with Service Version**
```bash
nmap -sS -sV -O -p- -T4 <target_IP>
```
**Aggressive OS Scan for Accurate Results**
```bash
nmap -sS -O --osscan-guess -p- <target_IP>
```
**Aggressive Version intensity Scanning for Accurate Results**
```bash
nmap -sS -sV - --version-itensity 8 -p- -T4 <target_IP>
```
----
**Nmap Scripting Engine (NSE)**

**Default Nmap Script Scan**:
```bash
nmap -sS -sC -p- -T4 <target_IP>
```
**Listing all the NSE Scripts:**
- Generally all the nse scripts will be stored in `/usr/share/nmap/scripts`
- We can see all the scripts in a categorized way 
- it includes enum , exploit , vuln , general scripts
- we can use grep to leverage our scan type
```bash
ls -al /usr/share/nmap/scripts/ | grep -e "http"
# This will list all nse scripts related to http service
ls -al /usr/share/nmap/scripts/ | grep -e "ftp"
# This will list all the nse scripts related to FTP Service
```
**Running Specific Script Scan :**
```bash
nmap -sS --script=<scriptname> -T4 -p- / -p(specified port) <target_ip>
```
**Running OS , Service Detecting , Default Script , Traceroute :**
```bash
nmap -sn -A -p- -T4 <target_IP>
```
**Running Multiple Script Scans:**
```bash
nmap -sS --script=<scriptname>,<scriptname> -p- -T4 <target_IP>
```
