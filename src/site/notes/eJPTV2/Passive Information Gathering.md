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
