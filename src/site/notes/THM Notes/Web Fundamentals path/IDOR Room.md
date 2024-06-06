---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/idor-room/","title":"IDOR - THM Walkthrough","tags":["web"]}
---

# Notes: TryHackMe IDOR Module

## Overview
The TryHackMe IDOR (Insecure Direct Object Reference) module teaches how to identify and exploit IDOR vulnerabilities in web applications. This is a critical skill for cybersecurity professionals, especially those preparing for certifications like eJPT. The module covers the following tasks:

1. Understanding what IDOR is.
2. Exploiting IDOR vulnerabilities through practical examples.
3. Recognizing encoded and hashed IDs.
4. Identifying IDOR vulnerabilities in unpredictable IDs.
5. Locating IDORs in web applications.
6. Conducting a practical IDOR exploitation exercise.

## Key Concepts and Tools

### What is IDOR?
- **Definition**: IDOR stands for Insecure Direct Object Reference. It is an access control vulnerability that occurs when an application does not verify the identity of a user requesting access to objects (files, data, documents).
- **Example**: If a URL parameter such as `user_id=123` can be modified to `user_id=124` to access another user's information, an IDOR vulnerability exists.

### Exploiting IDOR Vulnerabilities
- **Example Process**:
  1. **Identify a URL with a numeric ID**: `http://example.com/profile?user_id=123`
  2. **Change the ID**: Modify the URL to `http://example.com/profile?user_id=124` to see if another user's information is accessible.

### Finding IDORs in Encoded IDs
- **Concept**: Web developers often encode IDs to ensure data integrity during transmission.
- **Common Encoding Technique**: Base64 encoding.
- **Tool**: Online Base64 encoders/decoders.
  - **Decoding**: Use `https://www.base64decode.org/`
  - **Encoding**: Use `https://www.base64encode.org/`

### Finding IDORs in Hashed IDs
- **Concept**: IDs might be hashed using algorithms like MD5.
- **Tool**: Online hash cracking services such as `https://crackstation.net/`
- **Example**:
  - A hashed ID like `202cb962ac59075b964b07152d234b70` can be cracked to reveal the original ID `123`.

### Finding IDORs in Unpredictable IDs
- **Concept**: IDs that do not follow a predictable pattern.
- **Method**: Create two accounts and swap the IDs to check for access control vulnerabilities.

### Where to Find IDORs
- **Potential Locations**: Address bar, AJAX requests, JavaScript files, hidden parameters in the application.
- **Techniques**: Parameter mining, inspecting network traffic, and checking unreferenced parameters.

## Practical Example Walkthrough

### Task 1: What is IDOR?
- **Answer**: Insecure Direct Object Reference

### Task 2: An IDOR Example
1. **Click on the View Site button**.
2. **Examine the URL structure in the email link**.
3. **Change the `ORDER ID` in the URL** to access different order details.
   - **Example**: Change `order_id=1234` to `order_id=1000`.
4. **Flag**: `THM{IDOR-VULN-FOUND}`

### Task 3: Finding IDORs in Encoded IDs
- **Common Encoding**: Base64
- **Answer**: base64

### Task 4: Finding IDORs in Hashed IDs
- **Common Hashing Algorithm**: MD5
- **Answer**: MD5

### Task 5: Finding IDORs in Unpredictable IDs
- **Minimum Accounts Needed**: 2
- **Answer**: 2

### Task 6: Where are IDORs Located?
- **Location Examples**: URL parameters, AJAX requests, JavaScript files.

### Task 7: A Practical IDOR Example
1. **Login** and navigate to the "Your Account" tab.
2. **Inspect the network traffic** using developer tools.
3. **Find the request URL** with the path `/api/v1/customer?id={user_id}`.
4. **Change the `user_id` parameter** to another user's ID to retrieve their information.
   - **Username for user_id 1**: `adam84`
   - **Email for user_id 3**: `j@fakemail.thm`

## Importance of Tools and Topics Discussed
- **Tools**: `curl`, Base64 encoders/decoders, hash cracking services.
- **Topics**: Understanding IDOR, encoding and decoding techniques, hashing algorithms.
- **Importance**: These tools and concepts are essential for identifying and exploiting IDOR vulnerabilities, a common issue in web applications.

## Conclusion
The IDOR module on TryHackMe provides a thorough understanding of how to find and exploit IDOR vulnerabilities. Mastering these techniques is crucial for cybersecurity professionals, particularly those preparing for certifications like eJPT. The practical examples and detailed explanations ensure a solid foundation in ethical hacking and web security.

### How the Attacks Were Performed
1. **Identify the Vulnerable Endpoint**: Locate the URL or parameter that can be manipulated.
2. **Modify the Parameter**: Change the ID to another user's ID to see if unauthorized access is granted.
3. **Analyze the Response**: Check if you can access another user's data.

### Logical Explanation
- **Trust Issue**: The server trusts user input without proper validation.
- **Lack of Access Control**: No verification of the user's identity before granting access to objects.
- **Exploitation**: Manipulating parameters to access unauthorized data.

By understanding and practicing these techniques, cybersecurity beginners can effectively identify and exploit IDOR vulnerabilities, enhancing their skills and knowledge for certifications like eJPT.