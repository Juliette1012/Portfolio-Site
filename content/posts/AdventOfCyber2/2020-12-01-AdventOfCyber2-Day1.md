---
title: AdventOfCyber2 Day 1
template: "post"
date: "2020-12-01"
draft: false
category: "Write-Ups, AdventOfCyber2"
tags:
  - "TryHackMe, AdventOfCyber2"
  - "Python"
social-image: "/media/adventOfCyber2/icon.png"
description: "It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)"
---

It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)

# Day 1 : A Christmas Crisis

We deploy the machine and go on the website with the IP address.

## What is the name of the cookie used for authentication?

We register on the website with a random login and password. For example : 
```
login : root
password : root0
```

We log in and with `F12` we acess to the cookies.  
The name of the cookie used for authentification is **auth**.

## In what format is the value of this cookie encoded ?

The value is : 
`7b22636f6d70616e79223a22546865204265737420466573746976616c20436f6d70616e79222c2022757365726e616d65223a226a756a75227d"` 
This cookie is encoded in **hexadecimal**.

## Having decoded the cookie, what format is the data stored in ?

We use : https://gchq.github.io/CyberChef/ and we put `from hex` to decode the cookie.
We found : `{"company":"The Best Festival Company", "username":"root"}`
It's a Java Script Object, so the data are stored in **json**.

## Figure out how to bypass the authentication. 
 * What is the value of Santa's cookie ?

We put `{"company":"The Best Festival Company", "username":"santa"}` into an hexadecimal encoder and find this value : 

`7b22636f6d70616e79223a22546865204265737420466573746976616c20436f6d70616e79222c2022757365726e616d65223a2273616e7461227d`

## Now that you are the santa user, you can re-activate the assembly line ! 
What is the flag you're given when the line is fully active ?**

We put this new cookie instead of the previous one, activate all the lines and refresh the page to see the flag : **THM{MjY0Yzg5NTJmY2Q1NzM1NjBmZWFhYmQy}**