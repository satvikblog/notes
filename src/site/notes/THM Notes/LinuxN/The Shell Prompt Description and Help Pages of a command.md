---
{"Section":2.1,"Status":"Complete","tags":["linux"],"title":"The Shell Prompt Description and Help Pages of a command - Linux","dg-publish":true,"permalink":"/thm-notes/linux-n/the-shell-prompt-description-and-help-pages-of-a-command/","dgPassFrontmatter":true}
---

# NOTES

---

- Prompt description contains the information like  
    > usernames  
    >Host Name  
    > Present working Directory  
    

`<username>@<hostname><current working directory>$`

![[usersworkspace.png\|usersworkspace.png]]

**Satvik** - Username

**Satvik** - Hostname

**~** indicates home directory and it is default for everyone

**$** - will tell that user is not logged in as root user nor have privileged permissions

**# -** indicates that user is logged in as a root user and have privileged permssions

![[root_user.png\|root_user.png]]

> In addition to providing basic information like the current user and  
> working directory, we can customize to display other information in the  
> prompt, such as the IP address, date, time, the exit status of the last  
> command, and more. This is especially useful for us during our  
> penetration tests because we can use various tools and possibilities  
> like  
> `script` or the `.bash_history` to filter and  
> print all the commands we used and sort them by date and time. For  
> example, the prompt could be set to display the full path of the current  
> working directory instead of just the current directory name, which can  
> also include the target’s IP address if we work organized.  
> 
> The prompt can be customized using special characters and variables in the shell’s configuration file (`.bashrc` for the Bash shell). For example, we can use: the `\u` character to represent the current username, `\h` for the hostname, and `\w` for the current working directory.
> 
> .
> 
> |   |   |
> |---|---|
> |**Special Character**|**Description**|
> |`\d`|Date (Mon Feb 6)|
> |`\D{%Y-%m-%d}`|Date (YYYY-MM-DD)|
> |`\H`|Full hostname|
> |`\j`|Number of jobs managed by the shell|
> |`\n`|Newline|
> |`\r`|Carriage return|
> |`\s`|Name of the shell|
> |`\t`|Current time 24-hour (HH:MM:SS)|
> |`\T`|Current time 12-hour (HH:MM:SS)|
> |`\@`|Current time|
> |`\u`|Current username|
> |`\w`|Full path of the current working directory|
> 
> we can use [https://bash-prompt-generator.org/](https://bash-prompt-generator.org/) website to customize our own terminal description screen

### Using MAN and APROPOS Commands:

Man is a tool in any linux based distro which will retrieve the manual page of the particular command / tool . In which we can learn and see the description of the command / tool and how to use it

![[man_sudo.png\|man_sudo.png]]

---

![[manpage.png\|manpage.png]]

As we can see that this is the Manual page of SUDO command  
not only MAN , we can also get it by executing  

```Bash
sudo --help
```

it will retrieve the same info

  

- Now we will see what is **Apropos  
      
    **> There is always a Small description of every tool or command out there in its man page . so in order to retrieve that we use apropos  
    > You can see it in below Picture  
    

![[apropos.png\|apropos.png]]