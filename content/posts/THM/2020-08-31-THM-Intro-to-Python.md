---
layout: post
title: Write-Up [THM] Intro to Python
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Python]
featured-image:  thm/intro-python/theme.png
featured-image-alt: Intro to Python
---

It's a write-up about the challenge of the room : [Try Hack Me - Room : Intro to Python](https://tryhackme.com/room/intrototopython)

# Challenge Time !

In the [Task 12], we deploy the instance.

* Enter the decoded flag to complete the room! 

The script `chal.py` decoded the string which is in the file `encodedflag.txt` to get the final flag. This one has been base64'd 5 times, based32'd 5 times and base16'd 5 times.  

## File chal.py

```
import base64

file = open("encodedflag.txt","r")

flag = file.read()


code = ""

for i in range(0,5):
	code = base64.b16decode(flag)
	flag = code

for i in range(0,5):
	code = base64.b32decode(flag)
	flag = code

for i in range(0,5):
	code = base64.b64decode(code)
	flag = code

print(flag)
file.close()
```

After executed the scipt `chal.py`, we obtained : `b'THM{d431ff8fea00ad3f6b685b7182078e73}'`.   So, the flag is `THM{d431ff8fea00ad3f6b685b7182078e73}=`.