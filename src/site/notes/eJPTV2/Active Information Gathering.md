---
{"dg-publish":true,"permalink":"/e-jptv-2/active-information-gathering/","title":"Active Information Gathering","tags":["ejptv2","information-gathering","nmap"]}
---

----
# DNS Zone Transfer 

+ In certain cases DNS server admins may want to copy or transfer zone files from one DNS server to another. This process is known as a zone transfer.
+ If misconfigured and left unsecured, this functionality can be abused by attackers to copy the zone file from the primary DNS server to another DNS server. 
+ A DNS Zone transfer can provide penetration testers with a holistic view of an organization's network layout. 
+ Furthermore, in certain cases, internal network addresses may be found on an organization's DNS servers.
+ Tools or utilities you can use 
  1. dig
  2. dnsenum
  3. fierce
  - **Usage:**
```bash
dig axfr @<ns> <domain>
dnsenum <domain name>
fierce -d < domain name>
```
---
# Host Discovery with nmap

- This is used to enumerate the devices connected to your local network 
- we can use `nmap ` tool to do this by using a ping scan 
- usage : 
```bash
nmap -sn 192.168.20.0/24 [ YOUR IP ADDRESS ]
```

-----

# Port Scanning with nmap

#### We can use nmap for various scans 

**Port Scan**:
```bash
sudo nmap -Pn 192.168.9.24 [TARGET IP]
```
**Specifying port range**:
```bash
sudo nmap -p1-2600 192.168.9.24 -Pn

-p- --> to scan all 65535 ports
-p80 --> to only scan port 80
-p80,445 --> to only scan port number 80 and 445

```
**Version Scan**:
```bash
sudo nmap -sV 192.168.9.3 -Pn -v

-v for verbose
# this scan will basically give you the information regarding the versions of the particular Services
```
**OS Detection:**
```bash
sudo nmap -sV -O 192.168.9.3 -Pn -v

-O - This detects the OS of that particular service
```
**Verbose / Limiting the speed of the scan**:
```bash
sudo nmap -sV -T4 -v 192.168.9.3 -Pn

-T4 : it is the speed limit of the scan ; T3 < T4 < T5
-v : will give you the real time scan report on the screen
```
**Script Scan**:
```bash
sudo nmap -sV -T4 -v -sC 192.168.9.3 -Pn

-sC --> it will enable script scan
this will enumerate more details and also we can specify the scripts individually
```
**Aggressive Scan**
```bash
sudo nmap -A 192.168.9.2 -Pn

-A : This agressive scan will combine the Script , OS , Version scans
-A = -sC , -sV , -O
```

-----
