---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/baisc-vuln/ssrf-room/","title":"SSRF Walkthrough - THM","tags":["web"]}
---

## TryHackMe SSRF Module Notes

### Overview
The TryHackMe SSRF (Server-Side Request Forgery) module teaches how to identify and exploit SSRF vulnerabilities in web applications. This is a critical skill for cybersecurity professionals, especially those preparing for certifications like eJPT. The module covers:

1. Understanding SSRF.
2. Viewing SSRF examples and practical exploitation.
3. Finding potential SSRF vulnerabilities.
4. Defeating common SSRF defenses.
5. Conducting a practical SSRF exploitation exercise.

### Key Concepts and Tools

#### What is SSRF?
- **Definition**: SSRF stands for Server-Side Request Forgery. It is a vulnerability that allows an attacker to make the server perform requests to unauthorized resources.
- **Types of SSRF**:
  - **Regular SSRF**: The response is returned to the attacker.
  - **Blind SSRF**: The attacker's screen does not receive any response.

#### Impact of SSRF
A successful SSRF attack can lead to:
- Access to unauthorized areas.
- Access to sensitive customer or organizational data.
- Ability to scale attacks to internal networks.
- Exposure of authentication tokens or credentials.

### Tasks and Answers

#### Task 1: What is an SSRF?
- **1. What does SSRF stand for?**
  - Answer: `Server-Side Request Forgery`
- **2. As opposed to a regular SSRF, what is the other type?**
  - Answer: `Blind`

#### Task 2: SSRF Examples
- **1. What is the flag from the SSRF Examples site?**
  - Navigate to the specified URL and retrieve the flag: `THM{SSRF_MASTER}`

#### Task 3: Finding an SSRF
- **1. What website can be used to catch HTTP requests from a server?**
  - Answer: `requestbin.com`

#### Task 4: Defeating Common SSRF Defenses
- **1. What method can be used to bypass strict rules?**
  - Answer: `Open Redirect`
- **2. What IP address may contain sensitive data in a cloud environment?**
  - Answer: `169.254.169.254`
- **3. What type of list is used to permit only certain input?**
  - Answer: `Allow List`
- **4. What type of list is used to stop certain input?**
  - Answer: `Deny List`

### Practical Example Walkthrough

#### Task 5: SSRF Practical

1. **Set Up**:
   - Create a customer account on the Acme IT Support website.
   - Navigate to the new avatar selection page.

2. **Inspect the Avatar Form**:
   - View the page source and inspect the avatar form.

3. **Manipulate the Form**:
   - Edit the value of the avatar field to `private`.
   - Submit the form to test the SSRF vulnerability.

4. **Bypass the Deny List**:
   - Use a directory traversal technique by setting the avatar value to `x/../private`.

5. **Retrieve and Decode the Flag**:
   - Decode the base64 content from the `/private` directory to get the flag: `THM{YOU_WORKED_OUT_THE_SSRF}`

### Importance of Tools and Topics Discussed

- **Tools**: 
  - HTTP logging tools like `requestbin.com`, `curl`, Burp Suite, CyberChef.
- **Topics**: 
  - Understanding SSRF and its impact.
  - Techniques for finding and exploiting SSRF vulnerabilities.
  - Methods for bypassing security defenses such as allow lists, deny lists, and open redirects.

### Conclusion
The SSRF module on TryHackMe provides a comprehensive understanding of SSRF vulnerabilities and how to exploit them. This knowledge is essential for cybersecurity professionals and is particularly valuable for those preparing for certifications like eJPT. The practical examples and detailed explanations ensure a solid foundation in ethical hacking and web security.

### How the Attacks Were Performed

1. **Identify the Vulnerable Endpoint**: Locate the URL or form field that can be manipulated.
2. **Modify the Parameter**: Change the URL or form field value to test for unauthorized access.
3. **Analyze the Response**: Check if the server responds with unauthorized data.

### Logical Explanation

- **Trust Issue**: The server trusts user input without proper validation.
- **Lack of Access Control**: The application does not verify the legitimacy of the requested resources.
- **Exploitation**: By manipulating input parameters, attackers can make the server perform unauthorized actions or access restricted data.

By mastering these techniques, cybersecurity beginners can effectively identify and exploit SSRF vulnerabilities, enhancing their skills and knowledge for certifications like eJPT.