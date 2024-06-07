---
{"dg-publish":true,"permalink":"/thm-notes/linux-n/linux-shell/","title":"Linux Shell","tags":["linux"]}
---

# NOTES

---

### What is a Shell ?

![[/Untitled 2.png\|Untitled 2.png]]

> **Shell Def**
> 
> A Linux terminal, also called a `shell` or command line,  
> provides a text-based input/output (I/O) interface between users and the  
> kernel for a computer system. The term console is also typical but does  
> not refer to a window but a screen in text mode. In the terminal  
> window, commands can be executed to control the system.  
> 
> We can think of a shell as a text-based GUI in which we enter  
> commands to perform actions like navigating to other directories,  
> working with files, and obtaining information from the system but with  
> way more capabilities.  

### Terminal Emulator

Terminal emulation is software that emulates the function of a  
terminal. It allows the use of text-based programs within a graphical  
user interface (  
`GUI`). There are also so-called command-line interfaces (`CLI`) that run as additional terminals in one terminal. In short, a terminal serves as an interface to the shell interpreter.

Terminal emulators and multiplexers are beneficial extensions for the  
terminal. They provide us with different methods and functions to work  
with the terminal, such as splitting the terminal into one window,  
working in multiple directories, creating different workspaces, and much  
more. An example of the use of such a multiplexer called Tmux could  
look something like this:  

![[Untitled 1.png\|Untitled 1.png]]

  

### The Shell :

The most commonly used shell in Linux is the `Bourne-Again Shell` (`BASH`),  
and is part of the GNU project. Everything we do through the GUI we can  
do with the shell. The shell gives us many more possibilities to  
interact with programs and processes to get information faster. Besides,  
many processes can be easily automated with smaller or larger scripts  
that make manual work much easier.  

Besides Bash, there also exist other shells like **[Tcsh/Csh](https://en.wikipedia.org/wiki/Tcsh)****,** **[Ksh](https://en.wikipedia.org/wiki/KornShell)****,** **[Zsh](https://en.wikipedia.org/wiki/Z_shell)****,** **[Fish](https://en.wikipedia.org/wiki/Friendly_interactive_shell)** shell and others.