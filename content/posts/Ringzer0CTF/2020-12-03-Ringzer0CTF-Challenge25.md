---
title: Ringzer0CTF Some Martian Message
template: "post"
date: "2020-12-03"
draft: false
category: "Write-Ups, Ringzer0CTF, Cryptography"
tags:
  - "Ringzer0CTF"
  - "Cryptography"
  - "CaesarCipher"
social-image: "/media/ringzer0CTF/icon.png"
description: "It's a write-up about the challenge : [Ringzer0CTF - Some Martian Message](https://ringzer0ctf.com/challenges/25)"
---

It's a write-up about the challenge : [Ringzer0CTF - Some Martian Message](https://ringzer0ctf.com/challenges/25)

# Challenge 25 - Some Martian Message

## 1. Challenge 

The first crypto challenge is : 

```SYNTPrfneVfPbbyOhgAbgFrpher```

## 2. Solution

The first thing we tried is a caesar cipher decryption tool, on this website :
http://www.xarg.org/tools/caesar-cipher/

This algorithm actually finds what kind of caesar encryption is used.
We chose "guess" as the key, and it found 13. 
So, the result was similar to an rol13 encryption, it's a Caesar cipher code. 

The code is : **FLAGCesarIsCoolButNotSecure**
