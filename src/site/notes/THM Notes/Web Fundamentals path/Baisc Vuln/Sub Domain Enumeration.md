---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/baisc-vuln/sub-domain-enumeration/","title":"Sub Domain Enumeration - THM Walkthrough","tags":["web"]}
---

### Subdomain Enumeration Notes

#### Importance of Subdomain Enumeration
Subdomain enumeration is crucial in cybersecurity as it helps to expand the attack surface, revealing potential points of vulnerability within a domain. By discovering subdomains, security professionals can uncover the hidden applications, services, or areas that might be susceptible to attacks, thereby enhancing the overall security posture of the domain.

### Techniques for Subdomain Enumeration

#### OSINT - SSL/TLS Certificates
**Description:** SSL/TLS certificates are issued by Certificate Authorities (CAs) and logged in Certificate Transparency (CT) logs. These logs are publicly accessible and can be used to discover subdomains associated with a domain.

**Tools:** 
- [crt.sh](https://crt.sh)
- [CT Search by Entrust](https://ui.ctsearch.entrust.com/ui/ctsearchui)

**Example Usage:**
- Search for a domain on crt.sh to find subdomains.
  
**Example Command:**
```plaintext
Search for "tryhackme.com" on crt.sh and find subdomains from the certificate logs.
```
**Example Output:**
- Domain: `store.tryhackme.com` (Logged on 2020-12-26)

#### OSINT - Search Engines
**Description:** Search engines index trillions of links, including subdomains. Using advanced search operators, one can narrow down results to find subdomains.

**Tools:**
- Google

**Example Usage:**
- Use the search term `-site:www.domain.com site:*.domain.com` on Google to find subdomains.

**Example Command:**
```plaintext
-site:www.tryhackme.com site:*.tryhackme.com
```
**Example Output:**
- Subdomain: `store.tryhackme.com`

#### DNS Bruteforce
**Description:** DNS Bruteforce involves trying numerous possible subdomains from a predefined list to discover valid subdomains. This method requires automation due to the high number of requests.&

**Tools:**
- dnsrecon

**Example Usage:**
- Use dnsrecon to perform a DNS bruteforce on a target domain.

**Example Command:**
```plaintext
Run dnsrecon and find subdomains for `acmeitsupport.thm`.
```
**Example Output:**
- Subdomain: `api.acmeitsupport.thm`

#### OSINT - Sublist3r
**Description:** Sublist3r automates OSINT subdomain discovery methods, aggregating data from multiple sources to quickly find subdomains.

**Tools:**
- [Sublist3r](https://github.com/aboul3la/Sublist3r)

**Example Usage:**
- Run Sublist3r to discover subdomains.

**Example Command:**
```plaintext
sublist3r -d acmeitsupport.thm
```
**Example Output:**
- Subdomain: `web55.acmeitsupport.thm`

#### Virtual Hosts
**Description:** Some subdomains are not publically accessible via DNS but can be found by manipulating the Host header. This method automates the process using a wordlist of common subdomains.

**Tools:**
- ffuf

**Example Usage:**
- Use ffuf to discover subdomains by manipulating the Host header.

**Example Command:**
```plaintext
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.186.57 -fs 2395
```
**Example Output:**
- Subdomain 1: `delta.acmeitsupport.thm`
- Subdomain 2: `yellow.acmeitsupport.thm`

### Example Commands and Tools Summary

- **SSL/TLS Certificates:**
  - **Tool:** crt.sh
  - **Command:** Search for a domain on crt.sh
  
- **Search Engines:**
  - **Tool:** Google
  - **Command:** `-site:www.domain.com site:*.domain.com`

- **DNS Bruteforce:**
  - **Tool:** dnsrecon
  - **Command:** `dnsrecon -d domain.com -D /path/to/wordlist`

- **Sublist3r:**
  - **Tool:** Sublist3r
  - **Command:** `sublist3r -d domain.com`

- **Virtual Hosts:**
  - **Tool:** ffuf
  - **Command:** `ffuf -w /path/to/wordlist -H "Host: FUZZ.domain.com" -u http://IP_ADDRESS -fs {size}`

### Importance of Subdomain Enumeration Techniques
Each of these techniques provides a unique approach to discovering subdomains, leveraging different data sources and methods. Combining these techniques ensures a comprehensive enumeration process, increasing the likelihood of finding all potential subdomains and thus securing the domain more effectively.

<a href="https://blog.satvik.live/post/THM%2FWEB%2FSub-Domain-Enumeration-THM-Walkthrough" style="text-decoration:none;">
  <button style="
    background: linear-gradient(90deg, rgba(0,123,255,1) 0%, rgba(0,102,204,1) 100%);
    border: none; /* Remove borders */
    color: white; /* White text */
    padding: 10px 20px; /* Some padding */
    text-align: center; /* Centered text */
    text-decoration: none; /* Remove underline */
    display: flex; /* Use flexbox */
    align-items: center; /* Center items vertically */
    justify-content: center; /* Center items horizontally */
    font-size: 16px; /* Increase font size */
    margin: 4px 2px; /* Add some margin */
    cursor: pointer; /* Add a pointer on hover */
    border-radius: 12px; /* Rounded corners */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); /* Add shadow */
    transition: transform 0.2s; /* Animation for hover effect */
    height: 40px; /* Fixed height for better alignment */
  " onmouseover="this.style.transform='scale(1.05)';" onmouseout="this.style.transform='scale(1.0)';">
    View Walkthrough 👀
  </button>
</a>
----
[[Satvik's Hacking Garden\|Satvik's Hacking Garden]]