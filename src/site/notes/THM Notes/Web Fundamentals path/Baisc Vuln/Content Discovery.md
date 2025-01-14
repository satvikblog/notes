---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/baisc-vuln/content-discovery/","title":"Content Discovery - THM Walkthrough","tags":["web"]}
---

# Content Discovery Techniques and Their Importance in Web Application Security

## What Is Content Discovery?
Content discovery in the context of web application security involves identifying hidden or non-obvious content on a website that was not intended for public access. This content can include files, videos, pictures, backup files, configuration files, administrative portals, older versions of the website, and more. Discovering such content is crucial for penetration testers to identify potential vulnerabilities and security risks.

Content discovery can be performed through three main methods:
1. **Manual Discovery**
2. **Automated Discovery**
3. **OSINT (Open-Source Intelligence)**

### Manual Discovery Techniques

#### Robots.txt
The `robots.txt` file is used by websites to tell search engines which pages should not be crawled. This file can provide penetration testers with valuable information about directories and files that the website owner does not want to be publicly accessible.

**Command:**
```
curl http://MACHINE_IP/robots.txt
```

**Example:**
```plaintext
Disallow: /staff-portal
```
This indicates that the `/staff-portal` directory is restricted from search engines.

#### Favicon
Favicons are small icons displayed in the browser's address bar. If a website uses a default favicon from a framework, it can give clues about the technologies in use.

**Command to get MD5 hash of the favicon:**
```
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```

Using the OWASP favicon database, the MD5 hash can be matched to identify the framework.

#### Sitemap.xml
The `sitemap.xml` file provides a list of URLs that the website owner wants to be indexed by search engines. It can reveal hidden or obscure pages.

**Command:**
```
curl http://MACHINE_IP/sitemap.xml
```

**Example:**
```plaintext
<url><loc>http://example.com/s3cr3t-area</loc></url>
```
This indicates a secret area `/s3cr3t-area` on the website.

#### HTTP Headers
HTTP headers in responses can provide information about the web server software and other technologies in use.

**Command:**
```
curl http://MACHINE_IP -v
```

#### Framework Stack
Examining page source comments or other elements can reveal the framework used by a website. This information can be used to find specific vulnerabilities associated with that framework.

**Example:**
```html
<!-- Page generated by THM Web Framework 1.0 -->
```
This indicates the use of a specific web framework.

### OSINT Techniques

#### Google Hacking / Dorking
Using Google search operators to find specific types of information about a website. 

**Examples:**
- `site:example.com`
- `inurl:admin`
- `filetype:pdf`
- `intitle:admin`

#### Wappalyzer
An online tool and browser extension that identifies technologies used by a website, such as frameworks, CMS, payment processors, etc.

**Website:**
```
https://www.wappalyzer.com/
```

#### Wayback Machine
An archive service that stores historical snapshots of web pages, useful for uncovering old or changed content.

**Website:**
```
https://archive.org/web/
```

#### GitHub
Searching public repositories on GitHub can reveal source code, credentials, and other sensitive information related to a target website.

**Example Search:**
```
site:github.com "example.com"
```

#### S3 Buckets
Amazon S3 buckets can sometimes be misconfigured to allow public access. The URL format is typically `http(s)://{name}.s3.amazonaws.com`.

### Automated Discovery Techniques

#### Using Tools with Wordlists
Automated discovery involves using tools that make multiple requests to a web server to find hidden content. These tools often use wordlists to guess common file and directory names.

**Example Tools:**
- **ffuf**
  ```
  ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -u http://MACHINE_IP/FUZZ
  ```

- **dirb**
  ```
  dirb http://MACHINE_IP/ /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
  ```

- **Gobuster**
  ```
  gobuster dir --url http://MACHINE_IP/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
  ```

**Common Discoveries:**
- Directories: `/monthly`
- Log files: `development.log`

## Importance of Content Discovery
Content discovery is essential for identifying potential security vulnerabilities in a web application. By uncovering hidden or restricted content, penetration testers can:
- Identify sensitive files and directories that may be exposed.
- Discover outdated or vulnerable components.
- Understand the underlying technology stack.
- Find misconfigurations that could be exploited.

Effective content discovery enhances the security posture of a web application by allowing for the identification and remediation of hidden threats before they can be exploited by malicious actors.

<a href="https://blog.satvik.live/post/THM%2FWEB%2FContent-Discovery-THM-Walkthrough" style="text-decoration:none;">
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
    Visit Walkthrough 👀
  </button>
</a>
----
[[Satvik's Hacking Garden\|Satvik's Hacking Garden]]
