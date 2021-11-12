---
layout: post
title: Write-Up [THM] Introductory Researching
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Google]
featured-image:  thm/intro-research/theme.png
featured-image-alt: Introductory Researching
---

It's a write-up about the room : [Try Hack Me - Room : Introductory Researching](https://tryhackme.com/room/introtoresearch)

# [Task 1] Introduction

![Task 1](/assets/img/thm/intro-research/task-1.png)

# [Task 2] Example Research Question

We search in `google` to answer all this questions :

![Answers Task 2](/assets/img/thm/intro-research/answers-2.png)

# [Task 3] Vulnerability Searching

> Often in hacking you'll come across software that might be open to exploitation. For example, Content Management Systems (such as Wordpress, FuelCMS, Ghost, etc) are frequently used to make setting up a website easier, and many of these are vulnerable to various attacks. So where would we look if we wanted to exploit specific software?

The answer to that question lies in website such as : 
* ![ExploitDB](https://www.exploit-db.com)
* ![NVD](https://nvd.nist.gov/vuln/search)
* ![CVE Mitre](https://cve.mitre.org)

> `NVD` keeps track of CVEs (Common Vulnerabilities and Exposures) -- whether or not there is an exploit publicly available -- so it's a really good place to look if you're researching vulnerabilities in a specific piece of software. CVEs take the form: CVE-YEAR-IDNUMBER

> `ExploitDB` tends to be very useful for hackers, as it often actually contains exploits that can be downloaded and used straight out of the box. It tends to be one of the first stops when you encounter software in a CTF or pentest.

![Answers Task 3](/assets/img/thm/intro-research/answers-3.png)

# [Task 4] Manual Pages

`Manual pages` are available with the `man` command. They give access directly in the terminal to the manual pages for most tools.

![Answers Task 4](/assets/img/thm/intro-research/answers-4.png)