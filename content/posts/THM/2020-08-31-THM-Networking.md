---
title: Write-Up [THM] Networking
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Networking"
  - "subnet"
  - "cisco"
  - "routing"
social-image: "/media/thm/networking/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : Networking](https://tryhackme.com/room/bpnetworking)"
---

It's a write-up about the room : [Try Hack Me - Room : Networking](https://tryhackme.com/room/bpnetworking)

# [Task 1] - Kinda like a street adress, just cooler

> In a manner similar to streets and homes, computers and their respective communication networks must have a way to address their 'mail'. In the following set of questions, we'll investigate the various types of IPv4 addresses.

![Task 1](/media/thm/networking/task-1.png)

* How many categories of IPv4 addresses are there? `5`

* Which type is for research? Looking for a letter rather than a number here. `E`

* How many private address ranges are there? `3`

* Which private range is typically used by businesses? `A`

*  There are two common default private ranges for home routers, what is the first one? `192.168.0.0`

* How about the second common private home range? `192.168.1.0`

* How many addresses make up a typical class C range? Specifically a /24. `256`

* Of these addresses two are reserved, what is the first addresses typically reserved as? `Network`

* The very last address in a range is typically reserved as what address type? `Broadcast`

* A third predominant address type is typically reserved for the router, what is the name of this address type? `Gateway`

* Which address is reserved for testing on individual computers? `127.0.0.1`

* A particularly unique address is reserved for unroutable packets, what is that address? This can also refer to all IPv4 addresses on the local machine. `0.0.0.0`

# [Task 2] - Binary to Decimal

![Task 2](/media/thm/networking/task-2.png)

We convert this following binary values into decimal.

* 1001 0010 `146`

* 0111 0111 `119`

* 1111 1111 `255`

* 1100 0101 `197`

* 1111 0110 `246`

* 0001 0011 `19`

* 1000 0001 `129`

* 0011 0001 `49`

* 0111 1000 `120`

* 1111 0000 `240`

* 0011 1011 `59`

* 0000 0111 `7`

# [Task 3] - Decimal to Binary

We convert this following decimal numbers into binary decimals.

* 238 `11101110`

* 34 `00100010`

* 123 `01111011`

* 50 `00110010`

* 255 `11111111`

* 200 `11001000`

* 10 `00001010`

* 138 `10001010`

* 1 `00000001`

* 13 `00001101`

* 250 `11111010`

* 114 `01110010`

# [Task 4] - Address Class Identification

Using the table provided in [Task 1], we identify which class each of the following addresses belong to.

* 10.240.1.1 `A`

* 150.10.15.0 `B`

* 192.14.2.0 `C`

* 148.17.9.1 `B`

* 193.42.1.1 `C`

* 126.8.156.0 `A`

* 220.200.23.1 `C`

* 220.200.23.1 `D`

* 177.100.18.4 `B`

* 119.18.45.0 `A`

* 117.89.56.45 `A`

* 215.45.45.0 `C`