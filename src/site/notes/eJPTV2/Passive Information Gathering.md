---
{"dg-publish":true,"permalink":"/e-jptv-2/passive-information-gathering/","title":"Passive Information Gathering","tags":["ejptv2","information-gathering"]}
---

-----

## Website Recon && Foot printing techniques

1. **Resolving Web IP ADDRESS**
- if we want to perform recon on any website then the first thing we can looking into is retrieving the website's `IP ADDRESS`
- We can resolve websites IP ADDRESS by a command called 
  **`HOST`** 
  **Usage :**  ` host <web url> `
  **Example:** 
  ![Pasted image 20240802210456.png](/img/user/eJPTV2/Images/Pasted%20image%2020240802210456.png)
- If it shows more than one IP Address for a particular website , we should understand that website is using a proxy / firewall on it .
----
2. **Personal Information Recon**
- Next thing we are gonna look at is for any emails , names , contact details of the website owners/developers
- We can search in page contact forms , footers and header menu 
------
3. **Robots.txt** **& sitemap.xml**
- Robots.txt is essentially a main page / area that we must checkout for any website 
- It is basically a thing which defines or tells the search engines which pages in the website that a search engine should crawl through and which pages that it shouldn't when indexing the website on the search engine
- It may give you the potential information like which pages that general website visitors should not have access to and which pages they have access to .
- So that we can know some potential sensitive information of the website 
- Sitemap.xml is a file which gives us the structure of the website like pages , menu , submenu and navigation of the site completely
-----
4. **Browser Extensions & CLI Utilities**
- Another interesting technique to know much more about a website like what technologies the websites are running , their versions , status , and all tech stack for that website can be retrieved through some cool browser extension called :
  - **[`Builtwith`](https://chromewebstore.google.com/detail/builtwith-technology-prof/dapjbgnjinbpoindlpdmhochffioedbn)** 
  - **[`wappanalyzer`](https://chromewebstore.google.com/detail/wappalyzer-technology-pro/gppongmhjkpfnbhagpmjfkannfbllamg)**
  - **CLI utility :** `whatweb`
    - example usage : `whatweb satvik.live`
    - ![Pasted image 20240802221256.png](/img/user/eJPTV2/Images/Pasted%20image%2020240802221256.png)
---------
5. **Downloading the website Source code for Analyzing** 
   - We can download the websites source code for analyzing it by using a tool called `HTTtrack`
     `[httrack]`(https://www.httrack.com/)
   - This will download the entire website and we can go through the source and can analyze it so that we might have chance to discover any potential vulnerabilities 
------------
# Whois Enumeration

- whois is an internet protocol or an utility which is generally used enumerate the details of the particular domain name like its domain registrar info , created date , expiration date , contact details if any ...
- ![Pasted image 20240805212442.png](/img/user/eJPTV2/Images/Pasted%20image%2020240805212442.png)

- you can also use the online platforms like 
  - [WHO.IS](https://who.is)
  - [WHOIS.COM](https://www.whois.com/)
-----
# Website Recon and Footprinting using Netcraft

- Netcraft is an another open-source tool or utility that basically provides the whois info , Technology stack of that website , SSL / TLS info , Any vulnerabilities etc..
     [Netcraft](https://www.netcraft.com/)
-----
# DNS RECON

- DNS  **reconnaissance** is used to gather the info of the particular domains DNS Server like its 
  - A record
  - AAAA Record
  - MX record
  - NS Record
  - TXT record
  - SRV Record 
- We can use in build utility called `dnsrecon` in KALI LINUX 
  Usage : `dnsrecon -d <domain_name>`
- We can also use the site [DNS DUMPSTER](https://dnsdumpster.com)
- ![Pasted image 20240805220402.png](/img/user/eJPTV2/Images/Pasted%20image%2020240805220402.png)
- ![Pasted image 20240805220424.png](/img/user/eJPTV2/Images/Pasted%20image%2020240805220424.png)
------
# WAF with WAFw00f

- WAF - Web Application Firewall
- Using WAFw00f utility we can see whether the particular site is running behind any particular firewall or not so we can strategize our next moves accordingly 
- ![Pasted image 20240805221418.png](/img/user/eJPTV2/Images/Pasted%20image%2020240805221418.png)
-----
# Subdomain Enumeration with Sublist3r

- Subdomain enumeration is used to find any subdomains of a particular domain
- you can install it by `sudo apt-get install sublist3r` on your Kali Linux
- Usage : `sublist3r -d <domain_name`
  ex : `sublist3r -d satvik.live`
  ![Pasted image 20240805223253.png](/img/user/Pasted%20image%2020240805223253.png)
  
---
# Google Dorking / Hacking

- Google dorks are techniques to get the search results about a particular thing / website or anything in a desired way like limiting it to something explicitly
- ex:
  site:ine.com intitle:admin - Narrows down the search to display the pages of title ADMIN within the ine.com 
  
  site:*.ine.com - narrow down the search results to only of ine.com which would display all the subdomains of the ine.com
  - You can use : [Exploit Database ](https://www.exploit-db.com/) - to see thousands of Dorks which is very useful while gathering the information 
-----
