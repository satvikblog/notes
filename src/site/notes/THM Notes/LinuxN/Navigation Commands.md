---
{"Section":2.3,"Status":"Complete","tags":["linux"],"title":"Navigation Commands - Linux","dg-publish":true,"permalink":"/thm-notes/linux-n/navigation-commands/","dgPassFrontmatter":true}
---

# NOTES

---

As we navigate through different folders , files on our windows or android system by just clicking on them . But when we connect to them remotely via SSH we will have CLI in which we dont have GUI , so there is no chance to click on the directories / files to navigate through them . So navigation commands are most important

|Command|Purpose|
|---|---|
|pwd|tells the present working directory or in which directory we are in|
|ls|it will lists the files that are present in the directory|
|cd|it will make us to change the directory i.e navigate to different folders|
|cd ..|it will step back us to the previous folder that we came from / simply back click|

There are also some special flags that can be used with ls command that will extend the functionality of **ls** command

ls -l will display more information of each file and directory out there like  
> Permissions of the particular file  
> Size of the file  
> user and group that can access that file  
> Date and time the file is created  

![[lslaa.png\|lslaa.png]]

|   |   |
|---|---|
|**Column Content**|**Description**|
|`drwxr-xr-x`|Type and permissions|
|`satvik`|Owner of the file/directory|
|`satvik`|Group owner of the file/directory|
|`21`|Size of the file or the number of blocks used to store the directory information|
|`12 Nov 00:38`|Date and time|
|`Desktop`|Directory name|

we can see the hidden files of that directory by executing

```Bash
ls -la
```

We can clear the whole thing on Terminal when it gets messy by simply executing ‘clear’ command or using CTRL+L Shortcut.

We can get the history of the commands we have executed so far by using ‘history command ‘ or CTRL+R Shortcut

  

---

- **The Whole thing on HTB**
    
    # Navigation
    
    Navigation is essential, like working with the mouse as a standard  
    Windows user. With it, we move across the system and work in directories  
    and with files, we need and want. Therefore, we use different commands  
    and tools to print out information about a directory or a file and can  
    use advanced options to optimize the output to our needs.  
    
    One of the best ways to learn something new is to experiment with it.  
    Here we cover the sections on navigating through Linux, creating,  
    moving, editing, and deleting files and folders, finding them on the  
    operating system, different types of redirects, and what file  
    descriptors are. We will also find shortcuts to make our work with the  
    shell much easier and more comfortable. We recommend experimenting on  
    our locally hosted VM. Ensure we have created a snapshot for our VM in  
    case our system gets unexpectedly damaged.  
    
    Let us start with the navigation. Before we move through the system,  
    we have to find out in which directory we are. We can find out where we  
    are with the command  
    `pwd`.
    
    ```Plain
    cry0l1t3@htb[~]$ pwd/home/cry0l1t3
    ```
    
    Only the `ls` command is needed to list all the contents  
    inside a directory. It has many additional options that can complement  
    the display of the content in the current folder.  
    
    ```Plain
    cry0l1t3@htb[~]$ lsDesktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
    ```
    
    Using it without any additional options will display the directories and files only. However, we can also add the `-l` option to display more information on those directories and files.
    
    ```Plain
    cry0l1t3@htb[~]$ ls -ltotal 32
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 Desktop
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Documents
    drwxr-xr-x 3 cry0l1t3 htbacademy 4096 Nov 15 03:26 Downloads
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Music
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Pictures
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Public
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Templates
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Videos
    ```
    
    First, we see the total amount of blocks (`512-byte`) used  
    by the files and directories listed in the current directory, which  
    indicates the total size used. That means it used 32 * 512-byte =  
    `16384 bytes` of disk space. Next, we see a few columns that are structured as follows:
    
    |   |   |
    |---|---|
    |**Column Content**|**Description**|
    |`drwxr-xr-x`|Type and permissions|
    |`2`|Number of hard links to the file/directory|
    |`cry0l1t3`|Owner of the file/directory|
    |`htbacademy`|Group owner of the file/directory|
    |`4096`|Size of the file or the number of blocks used to store the directory information|
    |`Nov 13 17:37`|Date and time|
    |`Desktop`|Directory name|
    
    However, we will not see everything that is in this folder. A  
    directory can also have hidden files that start with a dot at the  
    beginning of its name (e.g.,  
    `.bashrc` or `.bash_history`). Therefore, we need to use the command `ls -la` to `list all` files of a directory:
    
    ```Plain
    cry0l1t3@htb[~]$ ls -latotal 403188
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 .bash_history
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 .bashrc
    ...SNIP...
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:37 Desktop
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Documents
    drwxr-xr-x 3 cry0l1t3 htbacademy 4096 Nov 15 03:26 Downloads
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Music
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Pictures
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Public
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Templates
    drwxr-xr-x 2 cry0l1t3 htbacademy 4096 Nov 13 17:34 Videos
    ```
    
    To list the contents of a directory, we do not necessarily need to navigate there first. We can also use “`ls`” to specify the path where we want to know the contents.
    
    ```Plain
    cry0l1t3@htb[~]$ ls -l /var/total 52
    drwxr-xr-x  2 root root     4096 Mai 15 18:54 backups
    drwxr-xr-x 18 root root     4096 Nov 15 16:55 cache
    drwxrwsrwt  2 root whoopsie 4096 Jul 25  2018 crash
    drwxr-xr-x 66 root root     4096 Mai 15 03:08 lib
    drwxrwsr-x  2 root staff    4096 Nov 24  2018 local
    <SNIP>
    ```
    
    We can do the same thing to navigate to the directory. To move through the directories, we use the command `cd`. Let us change to the `/dev/shm` directory. Of course, we can go to the `/dev` directory first and then `/shm`. Nevertheless, we can also enter the full path and jump there.
    
    ```Plain
    cry0l1t3@htb[~]$ cd /dev/shmcry0l1t3@htb[/dev/shm]$
    ```
    
    Since we were in the home directory before, we can quickly jump back to the directory we were last in.
    
    ```Plain
    cry0l1t3@htb[/dev/shm]$ cd -cry0l1t3@htb[~]$
    ```
    
    The shell also offers us the auto-complete function, which makes navigation easier. If we now type `cd /dev/s` and press `[TAB] twice`, we will get all entries starting with the letter “`s`” in the directory of `/dev/`.
    
    ```Plain
    cry0l1t3@htb[~]$ cd /dev/s [TAB 2x]shm/ snd/
    ```
    
    If we add the letter “`h`” to the letter “`s`,” the shell will complete the input since otherwise there will be no folders in this directory beginning with the letters “`sh`”. If we now display all contents of the directory, we will only see the following contents.
    
    ```Plain
    cry0l1t3@htb[/dev/shm]$ ls -la /dev/shmtotal 0
    drwxrwxrwt  2 root root   40 Mai 15 18:31 .
    drwxr-xr-x 17 root root 4000 Mai 14 20:45 ..
    ```
    
    The first entry with a single dot (`.`) indicates the current directory we are currently in. The second entry with two dots (`..`) represents the parent directory `/dev`. This means we can jump to the parent directory with the following command.
    
    ```Plain
    cry0l1t3@htb[/dev/shm]$ cd ..cry0l1t3@htb[/dev]$
    ```
    
    Since our shell is filled with some records, we can clean the shell with the command `clear`. First, however, let us return to the directory `/dev/shm` before and then execute the `clear` command to clean up our terminal.
    
    ```Plain
    cry0l1t3@htb[/dev]$ cd shm && clear
    ```
    
    Another way to clean up our terminal is to use the shortcut `[Ctrl] + [L]`. We can also use the arrow keys (`↑` or `↓`)  
    to scroll through the command history, which will show us the commands  
    that we have used before. But we also can search through the command  
    history using the shortcut  
    `[Ctrl] + [R]` and type some of the text that we are looking for.