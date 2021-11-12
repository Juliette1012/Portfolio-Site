---
layout: post
title: Write-Up [THM] Learn Linux
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Linux, Bash]
featured-image:  thm/learn-linux/theme.png
featured-image-alt: Learn Linux
---

It's a write-up about the room : [Try Hack Me - Room : Learn Linux](https://tryhackme.com/room/zthlinux)

# [Section 1 : SSH]

We connect by ssh to the host **ip_machine** with the username and password : **shiba1**.  

We used the command : `ssh shiba1@ip_machine` with the password `shiba1`.

# [Section 2 : Running Commands]

To `output` hello without a newline : `echo -n hello`.

# [Section 3 : Basic File Operations]

* What flag outputs all entries ? `-a`

* What flag outputs things in a "long list" format ? `-l`

* What flag numbers all output lines ? `-n`

* How would you run a binary called hello using the directory shortcut ? `./hello`

* How would you run a binary called hello in your home directory using the shortcut ~ ? `~/hello`

* How would you run a binary called hello in the previous directory using the shortcut .. ? `../hello`

# Binary - shiba1

> This challenge is pretty simple, create a file called noot.txt. Once you're done run the binary and you'll be given the password for the user shiba2!

We created a file called `noot.txt`, and we run the binary shiba1 like `./shiba1`.

We obtained the flag : **pinguftw**.

# su

* How do you specify which shell is used when you login? `-s`

# Section 4 - Linux Operators

* How would you output twenty to a file called test ? `echo twenty > test`.  

> The command **>>** does mainly the same thing as >, with one key difference. >> appends the output of a command to a file, instead of erasing it.

> Meaning `&&` allows you to execute a second command after the first one has executed successfully.

* How would you set nootnoot equal to 1111 `export nootnoot=1111`.

* What is the value of the home environment variable ?  
We used the command `echo $HOME`, and we found **/home/shiba2**.

* The `|` operator allows you to take the output of a command and use it as input for a second command.

* The `;` operator works a lot like &&, however it does not require the first command to execute successfully.

# Binary - shiba2

* The binary is checking to see if the environment variable "test1234" exists, and if it's set equal to the current $USER environment variable.

We assigned the current `$USER` environment variable to the variable *test1234*.  
So, we did the commmand : `export test1234=$USER`.  
We have executed the binary and obtained the password **happynootnoises** for shiba3.


# [Section 5 - Advanced File Operators]

## chmod

* What permissions mean the user can read the file, the group can read and write to the file, and no one else can read, write or execute the file? `460`

* What permissions mean the user can read, write, and execute the file, the group can read, write, and execute the file, and everyone else can read, write, and execute the file ? `777`

## chown

* How would you change the owner of file to paradox ? `chown paradox file`

* What about the owner and the group of file to paradox ? `chown paradox:paradox file`

* What flag allows you to operate on every file in the directory at once? `-R`

## rm

* What flag deletes every file in a directory ? `-r`

## mv

* How would you move file to /tmp ? `mv file /tmp`

## cd && mkdir

* Using relative paths, how would you cd to your home directory. `cd /`

* Using absolute paths how would you make a directory called test in /tmp. `mkdir /tmp/test`

## ln

* How would I link /home/test/testfile to /tmp/test ? `ln /home/test/testfile /tmp/test`

## find

* How do you find files that have specific permissions? `-perm`

* How would you find all the files in /home ? `find /home`

* How would you find all the files owned by paradox on the whole system ? `find / -user paradox`

## grep

* What flag lists line numbers for every string found ? `-n`

* How would I search for the string boop in the file aaaa in the directory /tmp ? `grep boop /tmp/aaaa`

# Binary - Shiba3

> We've been through a lot in this section, and the challenge for this binary will reflect that. The first step is actually finding the binary, I'm not heartless though, so I'll give you the name of the binary. The name of the binary is shiba4. The actual binary will check for two things, it will be checking that there's a directory called test in your home directory, how you create that is up to you. It will also be checking that inside the directory there's a file called test1234.

We have searched the binary shiba4 with the command : `find /* | grep siba4`.  
We found a binary hidden in */opt/secret*. We executed the binary and found the password **test1234**.

# [Section 6 : Miscellaneous]

# sudo 

* How do you specify which user you want to run a command as ? `-U`

* How would I run whoami as user jen? `sudo -U jen whoami`

* How do you list your current sudo privileges(what commands you can run, who you can run them as etc.) ? `-l`

## adding users and group

* How would I add the user test to the group test ? `sudo usermod -a -G test test`

## important files and directories

* /etc/passwd - Stores user information - Often used to see all the users on a system. 
* /etc/shadow - Has all the passwords of these users. 
* /tmp - Every file inside it gets deleted upon shutdown - used for temporary files. 
* /etc/sudoers - Used to control the sudo permissions of every user on the system -.  
* /home - The directory where all your downloads, documents etc are. - The equivalent on Windows is C:\Users\<user>. 
* /root - The root user's home directory - The equivilent on Windows is C:\Users\Administrator. 
* /usr - Where all your software is installed. 
* /bin and /sbin - Used for system critical files - DO NOT DELETE. 
* /var - The Linux miscellaneous directory, a myriad of processes store data in /var. 
* `$PATH` - Stores all the binaries you're able to run - same as $PATH on Windows. 

# Bonus Challenge

* There's one flag on this machine and it's in /root/root.txt, everything you need to get there is in this room.

We searched a regular file that we didn't see before with all users : shiba1, shiba2, shiba3, shiba4. 
So, with the command `find /* -username shiba2 -type f 2>>/dev/null`. 
-type f : to just see regular file. 
2>>/dev/null : to don't see permission denied files.

We found the file **/var/log/test1234**.
We logged with shiba2 with `su shiba2`and the password `pinguftw`.  
After, we used `cat /var/log/test1234` and found : **nootnoot:notsofast**.  
We decided to switch to the user *nootnoot* with the password *notsofast*.  
We check if *nootnoot* can use sudo with the command : `sudo -s` and logged with *notsofast* again.
Yesss, this user can use sudo, it's over ! After that, we could open the file `/root/root.txt`.  
In that one, we obtained the hidden flag **ad91979868d06e19d8e8a9c28be56e0c**.