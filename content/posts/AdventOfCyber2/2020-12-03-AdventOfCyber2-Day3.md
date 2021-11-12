---
title: AdventOfCyber2 Day 3
template: "post"
date: "2020-12-03"
draft: false
category: "Write-Ups, AdventOfCyber2"
tags:
  - "TryHackMe, AdventOfCyber2"
  - "Python"
social-image: "/media/adventOfCyber2/icon.png"
description: "It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)"
---

It's a write-up about the room : [Try Hack Me - Room : AdventOfCyber2](https://tryhackme.com/room/adventofcyber2)

# Day 3 : Christmas Chaos

Deploy your AttackBox (the blue "Start AttackBox" button) and the tasks machine (green button on this task) if you haven't already. Once both have deployed, open Firefox on the AttackBox and copy/paste the machines IP (MACHINE_IP) into the browser search bar.

We deploy the machine and go on the website with the machine IP.

## Use BurpSuite to brute force the login form.  
* Use the following lists for the default credentials:

```
Username || Password
root	 ||	root
admin	 ||	password
user	 ||	12345
```

## Use the correct credentials to log in to the Santa Sleigh Tracker app. 
> Don't forget to turn off Foxyproxy once BurpSuite has finished the attack!

We use BurpSuite, try to log with some random credentials. 
This captured request will show up in the Proxy tab in BurpSuite.   
We right-click it, and click "Send to Intruder", in this tab `Intruder` we choose `Clustering Bomb` attack type. 

Then, in the positions tab, we choose to set 2 payloads : one for login, and one for password.
In the first payload list, we add `root` `admin` and `user`.
In the second payload, we add `root` `password` and `12345`.

Then, we click on `Start Attack`. 
The attack shows us that the lenght of the response of the website is less higher than the others for the credentials : 
`admin` with `12345`. 



## What is the flag?

We log on the website with this previously credentials, and discover the flag. 

**THM{885ffab980e049847516f9d8fe99ad1a}**