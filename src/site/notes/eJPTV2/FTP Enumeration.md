---
{"dg-publish":true,"permalink":"/e-jptv-2/ftp-enumeration/","title":"FTP Enumeration - eJPTv2","tags":["ejptv2","nmap","gardenEntry"]}
---

### Notes: FTP Enumeration with Metasploit

---

#### **Overview**

FTP (File Transfer Protocol) is a standard protocol used to transfer files between systems over a network. It operates on a client-server model, where the client initiates a connection to the server for file operations.

In this lab, we will explore **FTP enumeration** using the **Metasploit Framework** to gather information about the target FTP server and test for vulnerabilities.

---

### **Step-by-Step Guide**

---

#### **1. Verify Target Accessibility**

Ensure the target machine is reachable by performing a ping test.

**Command:**

```bash
ping -c 4 demo.ine.local
```

- The `-c 4` option sends 4 packets to the target host.
- A successful response confirms that the target is reachable.

---

#### **2. Launch Metasploit Framework**

Start the Metasploit console to begin enumeration.

**Command:**

```bash
msfconsole
```

---

#### **3. Identify the FTP Service Version**

Use the **`ftp_version`** module in Metasploit to identify the FTP server's version.

**Commands:**

```bash
use auxiliary/scanner/ftp/ftp_version
set RHOSTS demo.ine.local
run
```

- **`use auxiliary/scanner/ftp/ftp_version`**: Loads the FTP version scanner module.
- **`set RHOSTS demo.ine.local`**: Sets the target machine.
- **`run`**: Executes the module.

The result reveals the FTP server version. Example: `ProFTPD 1.3.5a`.

---

#### **4. Perform Brute-Force to Find FTP Credentials**

Load the **`ftp_login`** module to perform brute force and identify valid credentials.

**Commands:**

```bash
use auxiliary/scanner/ftp/ftp_login
set RHOSTS demo.ine.local
set USER_FILE /usr/share/metasploit-framework/data/wordlists/common_users.txt
set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
run
```

- **`set USER_FILE`**: Specifies the wordlist for usernames.
- **`set PASS_FILE`**: Specifies the wordlist for passwords.
- The result identifies valid credentials, e.g., `sysadmin:654321`.

---

#### **5. Test for Anonymous Logins**

Check if the FTP server allows anonymous access.

**Commands:**

```bash
use auxiliary/scanner/ftp/anonymous
set RHOSTS demo.ine.local
run
```

- If anonymous logins are disabled, the module will indicate this.

---

#### **6. Log in to the FTP Server**

Use the obtained credentials to log in to the FTP server.

**Command:**

```bash
ftp demo.ine.local
```

- Provide the username (`sysadmin`) and password (`654321`) when prompted.

Successful authentication grants access to the FTP server.

---

### **Conclusion**

In this lab, we:

- Verified the target machine's accessibility.
- Used Metasploit to enumerate the FTP service and identify its version.
- Performed brute-force to retrieve valid credentials.
- Tested for anonymous login capability.
- Logged into the FTP server using the identified credentials.

---

### **Advanced Techniques and Insights**

---

#### **1. Manual Enumeration Techniques**

If Metasploit is unavailable, manual enumeration can be performed:

- **Banner Grabbing**: Use `telnet` or `nc` to fetch the FTP banner. **Command:**
    
    ```bash
    nc demo.ine.local 21
    ```
    
- **Command Response Testing**: Use `ftp` command-line tool and attempt anonymous login manually:
    
    ```bash
    ftp demo.ine.local
    ```
    
    Enter `anonymous` as the username and any password.

---

#### **2. Exploitation of Vulnerabilities**

Certain versions of FTP servers (e.g., ProFTPD) may have vulnerabilities:

- Search for known exploits in Metasploit: **Command:**
    
    ```bash
    search proftpd
    ```
    
- Use exploit modules if available.

---

#### **3. Custom Wordlists**

Improve brute-force accuracy by using customized wordlists:

- **Create User Wordlist:**
    
    ```bash
    echo -e "admin\nuser\nsysadmin" > users.txt
    ```
    
- **Create Password Wordlist:**
    
    ```bash
    echo -e "123456\npassword\n654321" > passwords.txt
    ```
    

---

#### **4. Logging FTP Activity**

Capture FTP traffic for further analysis using tools like Wireshark or tcpdump.

**Command:**

```bash
tcpdump -i eth0 port 21 -w ftp_traffic.pcap
```

---

#### **5. Bypassing Brute-Force Protections**

- Use **timing options** to slow down brute force and avoid detection. Example: Hydra with delay:
    
    ```bash
    hydra -l sysadmin -P passwords.txt ftp://demo.ine.local -t 1 -w 5
    ```
    
    The `-t 1` sets one thread, and `-w 5` adds a 5-second delay.

---

#### **6. Further Analysis with Nmap**

Nmap scripts for FTP can provide additional insights: **Command:**

```bash
nmap -p 21 --script=ftp-* demo.ine.local
```

---

These advanced techniques supplement the basic enumeration process, providing deeper insights and enhancing your approach to FTP penetration testing. Let me know if you'd like to expand or tweak any section!