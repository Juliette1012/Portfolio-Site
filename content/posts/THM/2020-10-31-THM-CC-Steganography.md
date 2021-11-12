---
layout: post
title: Write-Up [THM] CC-Steganography
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Steganography]
featured-image:  thm/cc-steganography/theme.png
featured-image-alt: CC-Steganography
---

It's a write-up about the room : [Try Hack Me - Room : CC-Steganography](https://tryhackme.com/room/ccstego)

# [Task 2] - Steghide

* What argument allows you to embed data(such as files) into other files? `embed`

* What flag let's you set the file to embed ? `-ef`

* What flag allows you to set the "cover file"?(i.e  the jpg) `-cf`

* How do you set the password to use for the cover file? `-p`

* What argument allows you to extract data from files? `extract`

* How do you select the file that you want to extract data from? `-sf`

* Given the passphrase "password123", what is the hidden message in the included "jpeg1" file.

We used : `steghide extract -sf jpeg1.jpg` and `cat a.txt`. We found **pinguftw** flag.

# [Task 3] - zsteg

* How do you specify that the least significant bit comes first ? `--lsb`

* What about the most significant bit? `--msb`

* How do you specify verbose mode? `-v`

* How do you extract the data from a specific payload? `-E`

* In the included file "png1" what is the hidden message? We used `zsteg png1.png` and found **nootnoot$**.

* What about the payload used to encrypt it. `b1,bgr,lsb,xy`

# [Task 4] - Exiftool

* In the included jpeg3 file, what is the document name ? `Hello :)`

# [Task 5] - Stegoveritas

* How do you check the file for metadata? `-meta`

* How do you check for steghide hidden information ? `-steghide`

* What flag allows you to extract LSB data from the image? `-extractLSB`

* In the included image jpeg2 what is the hidden message? `kekekekek`

# [Task 6] - Spectograms

* What is the hidden text in the included wav2 file? `Google`

# The final Exam

* What is key 1? 

We used `exiftool` and found : `Document Name : "password=admin".`
After that we used `steghide extractt -sf exam1.jpeg` with the password `admin`.   
In the file `a.txt` created there is the key 1 : **superkeykey**.

* What is key 2 ? 

We examined the `key2.wav` in Sonic Visualizer and found `https://imgur.com/KTrtNI5`.  
Next : `zsteg --lsb KTrtNI5.png` and there is the key 2 : **fatality**.

* What is key 3 ?

For the key 3, we used `stegoveritas qrcode.png` and the key result is **killshot**.