---
title: Write-Up [THM] Nessus
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Security"
  - "Nessus"
  - "Scanning"
  - "Red Primer Series"
social-image: "/media/thm/nessus/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : Nessus](https://tryhackme.com/room/rpnessus)"
---

It's a write-up about the room : [Try Hack Me - Room : Nessus](https://tryhackme.com/room/rpnessus)

# [Task 1] Deploy !

![Task 1](/media/thm/nessus/task-1.png)

We deploy the instance.

# [Task 2] Installation

![Task 2](/media/thm/nessus/task-2.png)

# [Task 3] - Nessus Quiz 

* As we log into Nessus, we are greeted with a button to launch a scan, what is the name of this button? `New Scan`

* Nessus allows us to create custom templates that can be used during the scan selection as additional scan types, what is the name of the menu where we can set these? `Policies`

* Nessus also allows us to change plugin properties such as hiding them or changing their severity, what menu allows us to change this? `Plugin Rules`

* Nessus can also be run through multiple 'Scanners' where multiple installations can work together to complete scans or run scans on remote networks, what menu allows us to see all of these installations? `Scanners`

* Let's move onto the scan types, what scan allows us to see simply what hosts are 'alive'? `Host Discovery`

* One of the most useful scan types, which is considered to be 'suitable for any host'? `Basic Network Scan`

* Following a few basic scans, it's often useful to run a scan wherein the scanner can authenticate to systems and evaluate their patching level. What scan allows you to do this? `Credential Patch Audit`

* When performing Web App tests it's often useful to run which scan? This can be incredibly useful when also using nitko, zap, and burp to gain a full picture of an application. `Web Applications Tests`

# [Task 4] - Scanning !

* Create a new 'Basic Network Scan' targeting the deployed VM. What option can we set under 'BASIC' to set a time for this scan to run? This can be very useful when network congestion is an issue. `Schedule`

* Under discovery set the scan to cover ports 1-65535. What is this type called? `port scan (all ports)`

* As we are connected to the network via a VPN, it may be to our benefit to 'tone down' the scan a bit. What scan type can we change to under 'ADVANCED' for this lower bandwidth connection? `Scan low bandwidth links`

* After the scan completes, which 'Vulnerability' can we view the details of to see the open ports on this host? `Nessus Syn Scanner`

* There seems to be a chat server running on this machine, what port is it on? `6667`

* Looks like we have a medium level vulnerability relating to SSH, what is this vulnerability named? `SSH Weak Algorithms Supported`

* Looks like we have a medium level vulnerability relating to SSH, what is this vulnerability named? `Apache/2.4.99`

# [Task 5] Wait, there's mail ?

We can add `SMTP` functionality into your Nessus install.

![Task 5](/media/thm/nessus/task-5.png)

# [Task 6] - So you're telling me that's how you set up a web app...

* What is the plugin id of the plugin that determines the HTTP server type and version? `10107`

* What authentication page is discovered by the scanner that transmits credentials in cleartext? 	`login.php`

* What is the file extension of the config backup? `.bak`

* Which directory contains example documents? (This will be in a php directory) `/exernal/phpids/0.6/docs/examples`

* What vulnerability is this application susceptible to that is associated with X-Frame-Options? `ClickJacking`

* What version of php is the server using? `5.5.9-1ubuntu4.26`
