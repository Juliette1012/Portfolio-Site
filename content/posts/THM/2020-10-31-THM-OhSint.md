---
title: Write-Up [THM] OhSINT
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "CTF"
  - "OhSINT"
social-image: "/media/thm/ohsint/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : OhSINT](https://tryhackme.com/room/ohsint)"
---

It's a write-up about the room : [Try Hack Me - Room : OhSINT](https://tryhackme.com/room/ohsint)

What information can you possible get with just one photo ? The photo is **WindowsXP.jpg**.

We used the tool *exiftool* : `exiftool WindowsXP.jpg` and we discovered this information about the photo : 

```
ExifTool Version Number         : 12.01
File Name                       : WindowsXP.jpg
Directory                       : .
File Size                       : 229 kB
File Modification Date/Time     : 2020:07:27 20:34:27+02:00
File Access Date/Time           : 2020:07:27 21:49:09+02:00
File Inode Change Date/Time     : 2020:07:27 21:49:06+02:00
File Permissions                : rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
XMP Toolkit                     : Image::ExifTool 11.27
GPS Latitude                    : 54 deg 17' 41.27" N
GPS Longitude                   : 2 deg 15' 1.33" W
Copyright                       : OWoodflint
Image Width                     : 1920
Image Height                    : 1080
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 1920x1080
Megapixels                      : 2.1
GPS Latitude Ref                : North
GPS Longitude Ref               : West
GPS Position                    : 54 deg 17' 41.27" N, 2 deg 15' 1.33" W
```

We googled the copyright Owoodflint and we found this site : [Owoodfl1nt Github](https://github.com/OWoodfl1nt/people_finder). The readme showed us : 

```
Hi all, I am from London, I like taking photos and open source projects.
Follow me on twitter: @OWoodflint
This project is a new social network for taking photos in your home town.
Project starting soon! Email me if you want to help out: OWoodflint@gmail.com
```

We found also a blog : [OliverWoodFlint WordPress](https://oliverwoodflint.wordpress.com/author/owoodflint/). The presentation on it is : 

```
Hey 
Im in New York right now, so I will update this site right away with new photos!
```

The code source of the page revealed us this line :  
`<p style="color:#ffffff;" class="has-text-color">pennYDr0pper.!</p>`. 

And a twitter : [OwoodFlint](https://twitter.com/owoodflint?lang=fr). The profile picture of this account is a cat.
There is a post : 

```
From my house I can get free wifi ;D
Bssid: B4:5D:50:AA:86:41 - Go nuts!
```

On the website : [wigle](https://wigle.net) we entered the BSSID and on the city London by zooming we found the name of the Wifi : `UnileverWifi`


* What is this users avatar of? `cat`

* What city is this person in? `london`

* Whats the SSID of the WAP he connected to? 

* What is his personal email address? `OWoodflint@gmail.com`

* What site did you find his email address on? `github`

* Where has he gone on holiday? `new york`

* What is this persons password? `pennYDr0pper.!`