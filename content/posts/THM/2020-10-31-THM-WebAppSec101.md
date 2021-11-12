---
title: Write-Up [THM] WebAppSec 101
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "WebApplication"
social-image: "/media/thm/webappsec101/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : WebAppSec 101](https://tryhackme.com/room/webappsec101)"
---

It's a write-up about the room : [Try Hack Me - Room : WebAppSec 101](https://tryhackme.com/room/webappsec101)

# [Task 2] - Walking through the application

* What version of Apache is being used?

We used nmap to know ports opened : `nmap -sV -A ip_machine` 

```
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.4 (protocol 2.0)
| ssh-hostkey: 
|   2048 54:04:09:42:d3:f4:07:d7:9c:e9:30:93:72:94:61:29 (RSA)
|   256 b3:a0:94:10:30:fe:f8:3b:73:72:52:b4:c2:6b:22:3d (ECDSA)
|_  256 35:86:be:66:ea:d2:ac:63:40:3d:f5:94:88:3c:83:5d (ED25519)
80/tcp  open  http    Apache httpd 2.4.7 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-title: WackoPicko.com
111/tcp open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          43061/tcp   status
|   100024  1          45246/udp6  status
|   100024  1          45747/tcp6  status
|_  100024  1          57246/udp   status
```

The version of Apached used is **2.4.7**.

* What language was used to create the website? **php**

* What version of this langage is used ?

We ran : `curl -I http://10.10.55.117` to have some information about the website.

```
HTTP/1.1 200 OK
Date: Sat, 22 Aug 2020 12:06:44 GMT
Server: Apache/2.4.7 (Ubuntu)
X-Powered-By: PHP/5.5.9-1ubuntu4.24
Set-Cookie: PHPSESSID=oevcaecn9fkftt2ceg43rh2qj0; path=/
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
Pragma: no-cache
Content-Type: text/html
```

The version oh php used is **5.5.9**.

# [Task 4] - Authentication

* What is the admin username? **admin**

* What is the admin password?

We used hydra on kali linux to bruteforce the password : 

`hydra -l admin -P /usr/share/dirb/wordlists/small.txt ip_machine http-post-form "/admin/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" -V

* What is the name of the cookie that can be manipulated? **session**

* What is the name of the cookie that can be manipulated? 

After created an account, we could see that we could change the user with a number `ip_machine/users/sample.php?userid=1`. We changed the number to 11 and found the user **Bryce**.

* What is the corresponding password to the username? 

We tried **bryce** as password and it worked. 