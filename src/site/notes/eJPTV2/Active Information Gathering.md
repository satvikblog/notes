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
sudo nmap -Pn 185.199.109.153
```
Output : 
![Pasted image 20241220152135.png](/img/user/Pasted%20image%2020241220152135.png)
**Specifying port range**:
```bash
sudo nmap -p1-500 5.196.105.14 -Pn

-p- --> to scan all 65535 ports
-p80 --> to only scan port 80
-p80,445 --> to only scan port number 80 and 445
-p1-500 --. it will scan all ports between 1-500
and also perform service scan

```

Output : 
![Pasted image 20241220152908.png](/img/user/Pasted%20image%2020241220152908.png)
**Version Scan**:
```bash
sudo nmap -sV 5.196.105.14 -Pn -v

-v for verbose
-sV performs service version scan that means it will enumerate the services of that host and its versions
-Pn means it will perform ping scan so that it will treat all hosts are online and prevents blocking from the firewall
# this scan will basically give you the information regarding the versions of the particular Services
```
Output : 
![Pasted image 20241220153345.png](/img/user/Pasted%20image%2020241220153345.png)
**OS Detection:**
```bash
sudo nmap -O 5.196.105.14 -Pn

-O - This detects the OS of that particular service
-Pn means it will perform ping scan so that it will treat all hosts are online and prevents blocking from the firewall
```
Output : 
![Pasted image 20241220153603.png](/img/user/Pasted%20image%2020241220153603.png)
**Verbose / Limiting the speed of the scan**:
```bash
sudo nmap -sV -T4 -v 5.196.105.14 -Pn

-T4 : it is the speed limit of the scan ; T3 < T4 < T5
-v : will give you the real time scan report on the screen
```
Output : 
![Pasted image 20241220153732.png](/img/user/Pasted%20image%2020241220153732.png)
So it gives real time data while scanning 

**Aggresive OS Detection for Accurate details of Operating system :
```bash
nmap -sS -O --osscan-guess -p- 5.196.105.14

-sS performs SYN scan
--osscan-guess performs OS Detection on the site
-p- performs port scan against all ports ( 65535 )

```


**Aggressive Scan**
```bash
sudo nmap -A 192.168.9.2 -Pn

-A : This agressive scan will combine the Script , OS , Version scans
-A = -sC , -sV , -O
```

-----
**HOME** : [[Satvik's Hacking Garden\|Satvik's Hacking Garden]]
