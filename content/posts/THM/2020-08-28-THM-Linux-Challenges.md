---
title: Write-Up [THM] Linux Challenges
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Linux"
  - "Bash"
social-image: "/media/thm/linux-challenges/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : Linux Challenges](https://tryhackme.com/room/linuxctf)"
---

It's a write-up about the room : [Try Hack Me - Room : Linux Challenges](https://tryhackme.com/room/linuxctf)

# Task 1 - Linux Challenges Introduction

We log to the machine with the following credentials :  

```
Username: garry  
Password: letmein
```

* How many visible files can you see in garrys home directory?  

`ssh -l garry IP_MACHINE` and we write the password **letmein**. 
To see how many files there are in home directory we used the command `ls`. There are **3** files.

# Task 2 - The Basics

* What is flag 1 ?

To see the file **flag1** we use the command : `cat flag1.txt`

```
There are flags hidden around the file system, its your job to find them.

Flag 1: f40dc0cff080ad38a6ba9a1c2c038b2c

Log into bobs account to get flag 2.

Username: bob
Password: linuxrules
```

The flag 1 is **f40dc0cff080ad38a6ba9a1c2c038b2c**.

* What is flag 2 ?

We log into bob account with `su bob` and the password *linuxrules*.  
On the home directory bob, there is the file *flag2.txt*. On that one, there is the flag : **8e255dfa51c9cce67420d2386cede596**.

* Flag 3 is located where bob's bash history gets stored.

We use `history` on the terminal to see the history commands of Bob.  
The flag 3 is **9daf3281745c2d75fc6e992ccfdedfcd**.

* Flag 4 is located where cron jobs are created.

To list all scheduled cron jobs for the current user :`crontab -l`.  
The last line is `0 6 * * * echo 'flag4:dcd5d1dcfac0578c99b7e7a6437827f3' > /home/bob/flag4.txt`.  
So, the flag 4 is : **dcd5d1dcfac0578c99b7e7a6437827f3**.

* Find and retrieve flag 5.  

We search the **flag5** with `locate flag5`, we obtain the path : `/lib/terminfo/E/flag5.txt`.  
After that, to see the content of this file `cat /lib/terminfo/E/flag5.txt`.  
We find the flag 5 : **bd8f33216075e5ba07c9ed41261d1703**.

* "Grep" through flag 6 and find the flag. The first 2 characters of the flag is c9.

We locate the flag6. The path is `/home/flag6.txt` and we search the flag with the command : `cat home/flag6.txt | grap "c9"`.  
The flag6 is **c9e142a1e25b24a837b98db589b08be5**. 

* Look at the systems processes. What is flag 7.

To loof the system processes the command is `ps -aux` and we search the flag 7 so, `ps -aux | grep "flag7"` and we find **274adb75b337307bd57807c005ee6358**.

* De-compress and get flag 8.

First we locate the file : `/home/bob/flag8.tar.gz`.  
To extract files from a gz archive : `gunzip file.gz`.  
To extract all files from archive tar : `tar -xf file.tar`.  
We extract the file **flag8.txt** and use the command `cat` to see the flag : **75f5edb76fe98dd5fc9f577a3f5de9bc**. 

* By look in your hosts file, locate and retrieve flag 9.

Hosts file is locate in `/etc`. We use `cat etc/hosts` and see the line : `127.0.0.1	dcf50ad844f9fe06339041ccc0d6e280.com`.  
The flag 9 is **dcf50ad844f9fe06339041ccc0d6e280**.

* Find all other users on the system. What is flag 10.

We get a list of all users using the `/etc/passwd` file with cat or less.
In the list we find the flag **5e23deecfe3a7292970ee48ff1b6d00c**.

# Task 3 - Linux Functionality

* Run the command flag11. Locate where your command alias are stored and get flag 11.

A Bash alias is a method of supplementing or overriding Bash commands with new ones. They are often defined in $HOME/.bashrc or $HOME/bash_aliases (which must be loaded by $HOME/.bashrc).  
So, we see the file `.bashrc` and find the line : 

```
#custom alias
alias flag11='echo "You need to look where the alias are created..."' #b4ba05d85801f62c4c0d05d3a76432e0
```

The flag 10 is **b4ba05d85801f62c4c0d05d3a76432e0**.

* Flag12 is located were MOTD's are usually found on an Ubuntu OS. What is flag12?

The motd is a file on Unix-like systems that contains a "message of the day", used to send a common message to all users in a more efficient manner than sending them all an e-mail message. motd is stored in “/etc/update-motd.d/”.  
On this folder we find different files and on the first one : `00_header` we find the flag 12 : **01687f0c5e63382f1c9cc783ad44ff7f**.

* Find the difference between two script files to find flag 13.

To see the difference between two scripts : `diff`. So, `diff /home/bob/flag13/script1 /home/bob/flag13/script2` and the output is : 

```
2437c2437
< Lightoller sees Smith walking stiffly toward him and quickly goes to him. He yells into the Captain's ear, through cupped hands, over the roar of the steam... 
---
> Lightoller sees 3383f3771ba86b1ed9ab7fbf8abab531 Smith walking stiffly toward him and quickly goes to him. He yells into the Captain's ear, through cupped hands, over the roar of the steam... 
```

The flag 12 is **3383f3771ba86b1ed9ab7fbf8abab531**.

* Where on the file system are logs typically stored? Find flag 14.

There are stored in the `/var/log` directory. In this directory, there is the file `flagtourteen.txt`.  
In the last line we discover the flag **71c3a8ad9752666275dadf62a93ef393**. 

* Can you find information about the system, such as the kernel version etc. Find flag 15.

Information about the system is available in the file : `/etc/*release`. This one contains the line : `FLAG_15=a914945a4b2b5e934ae06ad6f9c6be45`.   
The flag 15 is **a914945a4b2b5e934ae06ad6f9c6be45**.

* Flag 16 lies within another system mount.

`/media` directory contains subdirectories of removable devices.  
We find th folder **cab4b7cae33c87794d82efa1e7f834e6** in `/media/f/l/a/g/1/6/is`.

* Login to alice's account and get flag 17. Her password is TryHackMe123. 

We swap to alice user : `su alice` with the password `TryHackMe123`.  
The file flag17 is on her dictory home and contains the flag **89d7bce9d0bab49e11e194b54a601362**.

* Find the hidden flag 18.

We use `locate flag18` to find the path of this file. We find : `/home/alice/.flag18` and using `cat .flag18` to see the flag.
The flag18 is **c6522bb26600d30254549b6574d2cef2**.

* Read the 2345th line of the file that contains flag 19.

We use the command : `sed '2345q;d' flag19` because `sed 'NUMq;d' file` where NUM is the number of the line you want to print.   
The flag is **490e69bd1bf3fc736cce9ff300653a3b**.

# Task 4 - Data Representation, Strings and Permissions

* Find and retrieve flag 20.

In the file flag20, we find `MDJiOWFhYjhhMjk5NzBkYjA4ZWM3N2FlNDI1ZjZlNjg=`. It seemed like a base64 code, so we decode the flag on this website [base64decode.org](https://www.base64decode.org/).  
The flag is **02b9aab8a29970db08ec77ae425f6e68**.

* Inspect the flag21.php file. Find the flag.

We locate this file in `/home/bob/flag21.php`. We use `chmod +x` to make it executable, and run it :  
```./flag21.php: line 1: syntax error near unexpected token `newline' 
<?='MoreToThisFileThanYouThink';?>'lag21_g00djob]`?>```

The flag21 is **g00djob**.

* Locate and read flag 22. Its represented as hex.

We locate this file in `/home/alice/flag22` : `39 64 31 61 65 38 64 35 36 39 63 38 33 65 30 33 64 38 61 38 66 36 31 35 36 38 61 30 66 61 37 64`. 
We decode it on the website [ConvertString](https://www.convertstring.com/fr/EncodeDecode/HexDecode) to obtain the flag : **9d1ae8d569c83e03d8a8f61568a0fa7d**.

* Locate, read and reverse flag 23.

We locate this file in `/home/alice/flag23` : `5ffb258330b8437a090c4f66507925ae`.  
After reversing it on the website [Reverse-String](https://codebeautify.org/reverse-string), we obtain the flag :
**ea52970566f4c090a7348b033852bff5**.

* Analyse the flag 24 compiled C program. Find a command that might reveal human readable strings when looking in the source code.

We locate this file in `/home/garry/flag24`.  
We analyse this file using `strings /home/garry/flag24 | grep "flag"`. We find 2 lines : 

```
flag24.c
flag_24_is_hidd3nStr1ng
```

Therefore, the flag is **hidd3nStr1ng**.

* Find flag 26 by searching the all files for a string that begins with 4bceb and is 32 characters long.

```
find / -xdev -type f -print0 2>/dev/null | xargs -0 grep -E ^[a-z0–9]{32} 2>/dev/null
```

We find the flag **4bceb76f490b24ed577d704c24d6955d**.

* Locate and retrieve flag 27, which is owned by the root user.

We locate this file file in : `/home/flag27`. We log with alice which is a `sudoer user`. After that, we used : `sudo cat /home/flag27`.
The flag is **6fc0c805702baebb0ecc01ae9e5a0db5**.

* Whats the linux kernel version? 

To see the linux kernel version, we use : `uname-a` and the version is **4.4.0-1075-aws**.

* Find the file called flag 29 and do the following operations on it:
```
    Remove all spaces in file.
    Remove all new line spaces.
    Split by comma and get the last element in the split.
cat /home/garry/flag29 | tr -d " \n" 
``` 

We use : `cat /home/garry/flag29 | tr -d " \n"` and we find **fastidiisuscipitmeaei**.

# Task 5 - SQL, FTP, Groups and RDP

* Use curl to find flag 30.  

`curl http://10.10.248.235` and the output is : `flag30:fe74bb12fe03c5d8dfc245bdd1eae13f`.  
So, the flag is **fe74bb12fe03c5d8dfc245bdd1eae13f**.

* Flag 31 is a MySQL database name.

```MySQL username: root
MySQL password: hello
```

We log in mysql with : `mysql -u root -p`.  
We want to know the database name, so `SHOW DATABASES;`. We find : 

```
+-------------------------------------------+
| Database                                  |
+-------------------------------------------+
| information_schema                        |
| database_2fb1cab13bf5f4d61de3555430c917f4 |
| mysql                                     |
| performance_schema                        |
| sys                                       |
+-------------------------------------------+
```

Th flag is **2fb1cab13bf5f4d61de3555430c917f4**.

* Bonus flag question, get data out of the table from the database you found above!

We use `use database_2fb1cab13bf5f4d61de3555430c917f4` and `show tables`. We can see the tables `flags`. Therefore, we do `select * from flags`.

```
+----+----------------------------------+
| id | flag                             |
+----+----------------------------------+
|  1 | ee5954ee1d4d94d61c2f823d7b9d733c |
+----+----------------------------------+
```

The bonus flag is : **ee5954ee1d4d94d61c2f823d7b9d733c**.

* Using SCP, FileZilla or another FTP client download flag32.mp3 to reveal flag 32

We use FileZilla with :
```
Protocol : SFTP - SSH File Transfer Protocol
Hôte : ip_machine
Port : 22
```
By listening the flag32.mp3, the flag is **tryhackme137**.

* Flag 33 is located where your personal PATH's are stored.

We try in Alice PATH first, anf after Bob. In Bob personal account, with `cat /home/bob/.profile` we find : `#Flag 33: 547b6ceee3c5b997b625de99b044f5cf`.  
Therefore, the flag is **547b6ceee3c5b997b625de99b044f5cf**.
