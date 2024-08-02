---
{"dg-publish":true,"permalink":"/satvik-s-hacking-garden/","tags":["gardenEntry"]}
---

# Hacking Notes by
## [Satvik Vemulapalli] 💌🧑‍💻

*I'll be sharing regular updates on my daily cybersecurity journey, diving into TryHackMe rooms and conquering HackTheBox machines*


> [!Author] About the Author
> An Aspiring Penetration tester pursuing B.Tech Third year
> Proficient in C , Python 
> Actively learning and exploring cybersecurity
> 
# Notes Index

| File                                                                                                                                       | Title                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| [[eJPTV2/What is Information Gathering\|What is Information Gathering]]                                                                 | Information Gathering                                            |
| [[eJPTV2/Pre-Requisite Knowledge\|Pre-Requisite Knowledge]]                                                                             | Networking Recap - eJPTv2                                        |
| [[THM Notes/Web Fundamentals path/Burp/Burpsuite -The Basics\|Burpsuite -The Basics]]                                                   | BurpSuite: The Basics- THM                                       |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Command Injection\|Command Injection]]                                                     | Command Injection                                                |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Cross site scripting XSS\|Cross site scripting XSS]]                                       | Intro to Cross Site Scripting                                    |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/IDOR Room\|IDOR Room]]                                                                     | IDOR - THM Walkthrough                                           |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Authentication Bypass\|Authentication Bypass]]                                             | Authentication Bypass - THM Walkthrough                          |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Sub Domain Enumeration\|Sub Domain Enumeration]]                                           | Sub Domain Enumeration - THM Walkthrough                         |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Content Discovery\|Content Discovery]]                                                     | Content Discovery - THM Walkthrough                              |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Walking an Application Module\|Walking an Application Module]]                             | Walking an Application - THM                                     |
| [[THM Notes/NMAP/Nmap Post Scan Commands\|Nmap Post Scan Commands]]                                                                     | Nmap Post Port Scans                                             |
| [[THM Notes/NMAP/Nmap Live Host Discovery\|Nmap Live Host Discovery]]                                                                   | Live Host Discovery - NMAP                                       |
| [[THM Notes/LinuxN/Backup and Restore\|Backup and Restore]]                                                                             | Backup And Restore -Linux                                        |
| [[THM Notes/LinuxN/Editing Files\|Editing Files]]                                                                                       | Editing Files - Linux                                            |
| [[THM Notes/LinuxN/Contanerization\|Contanerization]]                                                                                   | Contanerization Linux                                            |
| [[THM Notes/LinuxN/File Descriptors and redirections\|File Descriptors and redirections]]                                               | File Descriptors and Redirectors - Linux                         |
| [[THM Notes/LinuxN/File System Management\|File System Management]]                                                                     | File System Management - Linux                                   |
| [[THM Notes/LinuxN/Filter Contents\|Filter Contents]]                                                                                   | \-                                                               |
| [[THM Notes/LinuxN/Firewall setup\|Firewall setup]]                                                                                     | Firewall Setup - Linux                                           |
| [[THM Notes/LinuxN/Finding Files and Directories\|Finding Files and Directories]]                                                       | Finding Files and Directories                                    |
| [[THM Notes/LinuxN/Linux Distributions\|Linux Distributions]]                                                                           | Linux Distributions                                              |
| [[THM Notes/LinuxN/Linux Shell\|Linux Shell]]                                                                                           | Linux Shell                                                      |
| [[THM Notes/LinuxN/Linux Security\|Linux Security]]                                                                                     | Linux Security                                                   |
| [[THM Notes/LinuxN/Linux Structure\|Linux Structure]]                                                                                   | Linux Structure                                                  |
| [[THM Notes/LinuxN/Navigation Commands\|Navigation Commands]]                                                                           | Navigation Commands - Linux                                      |
| [[THM Notes/LinuxN/Linux vs Solaris\|Linux vs Solaris]]                                                                                 | Linux vs Solaris                                                 |
| [[THM Notes/LinuxN/Managing Permissions\|Managing Permissions]]                                                                         | Managing Permissions - Linux                                     |
| [[THM Notes/LinuxN/Working with Files and Directories\|Working with Files and Directories]]                                             | Working with Files and Directories                               |
| [[THM Notes/LinuxN/The Shell Prompt Description and Help Pages of a command\|The Shell Prompt Description and Help Pages of a command]] | The Shell Prompt Description and Help Pages of a command - Linux |
| [[THM Notes/NMAP/Nmap Advanced port scans\|Nmap Advanced port scans]]                                                                   | Nmap Advanced Port Scans                                         |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/File Inclusion - Web Hacking\|File Inclusion - Web Hacking]]                               | File Inclusion                                                   |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/SSRF Room\|SSRF Room]]                                                                     | SSRF Walkthrough - THM                                           |
| [[THM Notes/Web Fundamentals path/Baisc Vuln/Satvik's Hacking Garden Base\|Satvik's Hacking Garden Base]]                               | \-                                                               |

{ .block-language-dataview}
--------------------------------------------------
## Social Handles

- **Instagram**  [<img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram" width="15"/>](https://www.instagram.com/satvikshetty.v)
- **Github** [<img src="https://upload.wikimedia.org/wikipedia/commons/9/91/Octicons-mark-github.svg" alt="GitHub" width="20" style="filter: invert(100%)"/>](https://github.com/satvik-vs)
- **Linked In** [<img src="https://upload.wikimedia.org/wikipedia/commons/c/ca/LinkedIn_logo_initials.png" alt="LinkedIn" width="20" style="filter: invert(100%)"/>](https://www.linkedin.com/in/yourprofile)
--------------------------------------------------------------------------
## For more Information 👇

<a href="https://blog.satvik.live" style="text-decoration:none;">
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
    Visit my Blog 🧑‍💻
  </button>
</a>
<a href="https://satvik.live" style="text-decoration:none;">
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
     Visit my Portfolio
  </button>
</a>
<a href="mailto:contact@satvik.live" style="text-decoration:none;">
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
    Mail Me
  </button>
</a>