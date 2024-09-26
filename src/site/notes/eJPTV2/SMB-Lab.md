---
{"dg-publish":true,"permalink":"/e-jptv-2/smb-lab/","title":"SMB-Enumeration Lab","tags":["ejptv2","nmap"]}
---



---

### **Step 1: Initial Nmap Scan to Identify Open Ports**
- **Command**: `nmap demo.ine.local`
- **Output**:
  ```
  PORT    STATE SERVICE
  445/tcp open  microsoft-ds
  ```
- **Key Observations**: 
  - Port 445 is open, indicating that SMB (Server Message Block) service is running.
- **Why It’s Important**: Identifying open ports helps narrow down the services that need to be further investigated. SMB is widely used but often poorly secured, which makes it a valuable target.
- **Next Step**: Proceed with SMB-specific Nmap scripts to gather more information about the SMB service.

---

### **Step 2: SMB Protocol Enumeration**
- **Command**: `nmap -p445 --script smb-protocols demo.ine.local`
- **Output**:
  ```
  | smb-protocols: 
  |   dialects: 
  |     NT LM 0.12 (SMBv1) [dangerous, but default]
  |     2:0:2
  |     2:1:0
  |     3:0:0
  |_    3:0:2
  ```
- **Key Observations**:
  - SMBv1 (NT LM 0.12) is supported, which is **dangerous** and prone to exploits like **EternalBlue**.
- **Why It’s Important**: SMBv1 is outdated and vulnerable to known exploits. Observing this helps identify if the target is vulnerable to SMB-based attacks like EternalBlue.
- **Next Step**: Check for known SMB vulnerabilities (e.g., MS17-010) or escalate to brute-forcing or password spraying SMB accounts.

---

### **Step 3: SMB Security Mode Enumeration**
- **Command**: `nmap -p445 --script smb-security-mode demo.ine.local`
- **Output**:
  ```
  | smb-security-mode: 
  |   account_used: guest
  |   authentication_level: user
  |   message_signing: disabled (dangerous, but default)
  ```
- **Key Observations**:
  - **Guest** account is used, and **message signing is disabled**.
- **Why It’s Important**: Disabling SMB message signing leaves the server vulnerable to **man-in-the-middle (MITM)** attacks, where an attacker can intercept and modify SMB packets.
- **Next Step**: If the guest account can access shares, investigate them for sensitive data. Also, consider performing a MITM attack using tools like Responder.

---

### **Step 4: Enumerate SMB Sessions (Without Credentials)**
- **Command**: `nmap -p445 --script smb-enum-sessions demo.ine.local`
- **Output**:
  ```
  | smb-enum-sessions: 
  |   Users logged in:
  |     WIN-OMCNBKR66MN\bob since 2024-09-26T15:21:45
  ```
- **Key Observations**:
  - **Bob** is logged in, and no credentials were required to retrieve this information.
- **Why It’s Important**: Knowing which users are logged in allows targeting specific accounts. The absence of required credentials points to a misconfiguration.
- **Next Step**: Investigate the user 'bob' by trying password spraying or brute-forcing common passwords. Check if this user has any privileged access.

---

### **Step 5: Enumerate SMB Sessions (With Credentials)**
- **Command**:
  ```bash
  nmap -p445 --script smb-enum-sessions --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-enum-sessions: 
  |   Active SMB sessions:
  |     ADMINISTRATOR is connected from \\10.10.36.2
  ```
- **Key Observations**:
  - An **Administrator** session is active.
- **Why It’s Important**: An active session for an Administrator presents an opportunity for privilege escalation or lateral movement if further access to the account is gained.
- **Next Step**: Attempt to pivot using the Administrator session. Check for opportunities to dump credentials or escalate privileges further.

---

### **Step 6: Enumerate SMB Shares (Without Credentials)**
- **Command**: `nmap -p445 --script smb-enum-shares demo.ine.local`
- **Output**:
  ```
  | smb-enum-shares: 
  |   \\demo.ine.local\IPC$: 
  |     Anonymous access: READ/WRITE
  |   \\demo.ine.local\C$: 
  |     Current user access: READ
  ```
- **Key Observations**:
  - The **IPC$** share allows **anonymous access** with read/write privileges.
- **Why It’s Important**: The IPC$ share can be used to enumerate users and shares anonymously, making it a valuable entry point. The C$ share, although read-only, still gives insight into the file system structure.
- **Next Step**: Use tools like **smbclient** or **Metasploit** to list files and access data through these shares. Investigate for sensitive information, such as credentials, configuration files, etc.

---

### **Step 7: Enumerate SMB Shares (With Credentials)**
- **Command**:
  ```bash
  nmap -p445 --script smb-enum-shares --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-enum-shares: 
  |   \\demo.ine.local\C$: 
  |     Administrator access: READ/WRITE
  ```
- **Key Observations**:
  - The **C$ share** is accessible with **read/write privileges** using Administrator credentials.
- **Why It’s Important**: Gaining read/write access to C$ allows an attacker to upload malicious files or modify system files, potentially leading to full system compromise.
- **Next Step**: Investigate critical directories (like Windows/System32) to identify opportunities for escalating privileges. Consider uploading malicious payloads or creating scheduled tasks to gain persistence.

---

### **Step 8: Enumerate SMB Users**
- **Command**:
  ```bash
  nmap -p445 --script smb-enum-users --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-enum-users: 
  |   WIN-OMCNBKR66MN\Administrator
  |   WIN-OMCNBKR66MN\bob
  |   WIN-OMCNBKR66MN\Guest
  ```
- **Key Observations**:
  - Users **Administrator**, **bob**, and **Guest** exist on the system.
- **Why It’s Important**: This information helps in targeting specific users for further attacks. If the **Guest** account has any elevated privileges, it can be exploited.
- **Next Step**: Investigate the strength of the passwords for these users. Consider launching a brute-force attack on accounts like 'bob' and 'Guest'.

---

### **Step 9: Get SMB Server Statistics**
- **Command**:
  ```bash
  nmap -p445 --script smb-server-stats --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-server-stats: 
  |   Server statistics collected:
  |     Failed logins: 15063
  |     Files opened: 80
  ```
- **Key Observations**:
  - **15,063 failed login attempts** and **80 opened files**.
- **Why It’s Important**: A high number of failed login attempts may indicate an ongoing brute-force attack or misconfigurations. Open files may reveal important ongoing operations on the server.
- **Next Step**: Investigate if any successful login attempts have occurred recently, as this could indicate a compromised account.

---

### **Step 10: Enumerate SMB Domains**
- **Command**:
  ```bash
  nmap -p445 --script smb-enum-domains --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-enum-domains: 
  |   WIN-OMCNBKR66MN
  |     Domain name: WIN-OMCNBKR66MN
  ```
- **Key Observations**:
  - The machine is part of a domain **WIN-OMCNBKR66MN**.
- **Why It’s Important**: Knowing the domain structure helps in identifying if the target machine is part of a larger network, which can provide opportunities for **lateral movement**.
- **Next Step**: Explore domain trust relationships and identify domain controllers that can be targeted.

---

### **Step 11: Enumerate SMB Groups**
- **Command**:
  ```bash
  nmap -p445 --script smb-enum-groups --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-en

um-groups: 
  |   Builtin\Administrators (RID: 544): Administrator, bob
  |   Builtin\Users (RID: 545): bob
  |   Builtin\Guests (RID: 546): Guest
  ```
- **Key Observations**:
  - Users **Administrator** and **bob** are part of the **Administrators** group.
- **Why It’s Important**: Knowing which users have administrative privileges helps prioritize targets. If 'bob' has Administrator rights, compromising this account can lead to full control.
- **Next Step**: Attempt to crack or guess the passwords for these accounts. Escalate privileges using compromised credentials.

---

### **Step 12: List Files on SMB Shares**
- **Command**:
  ```bash
  nmap -p445 --script smb-ls --script-args smbusername=administrator,smbpassword=smbserver_771 demo.ine.local
  ```
- **Output**:
  ```
  | smb-ls: 
  |   Volume \\10.5.31.78\ADMIN$: 
  |     FILENAME: ADFS
  ```
- **Key Observations**:
  - Directories like **ADFS** were listed, indicating access to administrative files.
- **Why It’s Important**: Listing files on shared volumes can reveal sensitive files such as configuration files or passwords. Access to admin shares (like ADMIN$) is crucial for system takeover.
- **Next Step**: Look for files that contain sensitive information (e.g., password files, scripts, configuration files). You can also attempt to upload a payload for remote code execution.

---

### **Practical Use in eJPTv2 Exam**
For the **eJPTv2** exam, this step-by-step guide can be followed during an SMB enumeration task:
- Identify open ports and protocols.
- Enumerate shares, users, sessions, and domain information.
- Use findings to plan further attacks, such as password cracking, lateral movement, or privilege escalation.

