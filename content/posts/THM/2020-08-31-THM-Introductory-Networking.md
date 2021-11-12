---
title: Write-Up [THM] Introductory Networking
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Networking"
  - "OSI"
social-image: "/media/thm/intro-networking/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : Nessus](https://tryhackme.com/room/introtonetworking)"
---

It's a write-up about the room : [Try Hack Me - Room : Nessus](https://tryhackme.com/room/introtonetworking)

# [Task 1] Introduction

![Task 1](/media/thm/intro-networking/task-1.png)

# [Task 2] - The OSI Model : An Overview

![Task 2](/media/thm/intro-networking/task-2.png)

* Which layer would choose to send data over TCP or UDP? `4`

* Which layer checks received packets to make sure that they haven't been corrupted? `2`

* In which layer would data be formatted in preparation for transmission? `2`

* Which layer transmits and receives data? `1`

* Which layer encrypts, compresses, or otherwise transforms the initial data to give it a standardised format? `6`

* Which layer tracks communications between the host and receiving computers? `5`

* Which layer accepts communication requests from applications? `7`

* Which layer handles logical addressing? `3`

* When sending data over TCP, what would you call the "bite-sized" pieces of data? `3`

* [Research] Which layer would the FTP protocol communicate with? `7` 

* Which transport layer protocol would be best suited to transmit a live video? `UDP`

# [Task 3] - Encapsulation 

![Task 3](/media/thm/intro-networking/task-3.png)

* How would you refer to data at layer 2 of the encapsulation process (with the OSI model)? `Frames`

* How would you refer to data at layer 4 of the encapsulation process (with the OSI model), if the UDP protocol has been selected? `Datagrams`

* What process would a computer perform on a received message? `De-encapsulation`

* Which is the only layer of the OSI model to add a trailer during encapsulation? `Data Link`

* Does encapsulation provide an extra layer of security (Aye/Nay)? `Aye`

# [Task 4] - The TCP/IP Model

> The TCP/IP model is, in many ways, very similar to the OSI model. It's a few years older, and serves as the basis for real-world networking. The TCP/IP model consists of four layers: Application, Transport, Internet and Network Interface. Between them, these cover the same range of functions as the seven layers of the OSI Model.

![Task 4](/media/thm/intro-networking/task-4.png)

![Syn/ACK](/media/thm/intro-networking/syn-ack.png)

* Which model was introduced first, OSI or TCP/IP? `TCP/IP`

* Which layer of the TCP/IP model covers the functionality of the Transport layer of the OSI model (Full Name)? `Transport`

* Which layer of the TCP/IP model covers the functionality of the Session layer of the OSI model (Full Name)? `Application`

* The Network Interface layer of the TCP/IP model covers the functionality of two layers in the OSI model. These layers are Data Link, and?.. (Full Name)? `Physical`

* Which layer of the TCP/IP model handles the functionality of the OSI network layer? `Internet`

* What kind of protocol is TCP? `Connection-based`

* What is SYN short for? `Synchronise`

* What is the second step of the three way handshake? `SYN/ACK`

* What is the short name for the "Acknowledgement" segment in the three-way handshake? `ACK`

# [Task 5] - Wireshark

> We've gone over the basic theory -- now let's put it into practice! In this task we're going to look at some captured network traffic to see the advantages of understanding the OSI and TCP/IP Models.

`Wireshark` is a tool used to capture and analyse packets of data going across a network.

We're going to use Wireshark to get an idea of what these models look like in practice, with real world data.
We dowload the attached .pcap file (Wireshark capture).

![Task 5](/media/thm/intro-networking/task-5.png)

* What is the protocol specified in the section of the request that's linked to the Application layer of the OSI and TCP/IP Models? `Domain Name System`

* Which layer of the OSI model does the section that shows the IP address "172.16.16.77" link to (Name of the layer)? `Network`

* Which layer of the OSI model does the section that shows the IP address "172.16.16.77" link to (Name of the layer)? `User Datagram Protocol`

* Over what medium has this request been made (linked to the Data Link layer of the OSI model)? `Ethernet II`

* Over what medium has this request been made (linked to the Data Link layer of the OSI model)? `Physical`

* [Research] Can you figure out what kind of address is shown in the layer linked to the Data Link layer of the OSI model? `MAC`

# [Task 6] - Networking Tools : Ping

We're going to look at the `ping` command.

> The ping command is used when we want to test whether a connection to a remote resource is possible. Usually this will be a website on the internet, but it could also be for a computer on your home network if you want to check if it's configured correctly. Ping works using the ICMP protocol, which is one of the slightly less well-known TCP/IP protocols that I mentioned earlier. The ICMP protocol works on the Network layer of the OSI Model, and thus the Internet layer of the TCP/IP model. The basic syntax for ping is `ping <target>`.

* What command would you use to ping the bbc.co.uk website? `ping bbc.co.uk`

* Ping muirlandoracle.co.uk What is the IP address? `217.160.0.152`

* What switch lets you change the interval of sent ping requests? `-i`

* What switch would allow you to restrict requests to IPV4? `-4`

* What switch would give you a more verbose output? `-v`

# [Task 7] - Networking Tools : Traceroute

![Task 7](/media/thm/intro-networking/task-7.png)

* What switch would you use to specify an interface when using Traceroute? `-i`

* What switch would you use if you wanted to use TCP requests when tracing the route? `-T`

* [Lateral Thinking] Which layer of the TCP/IP model will traceroute run on by default? `Internet`

# [Task 8] - Networking Tools : WHOIS

`whois <domain>` to get a list of available information about the domain registration.

* What is the registrant postal code for facebook.com? `94025`

* When was the facebook.com domain first registered? `29/03/1997`

* Which city is the registrant based in? `Redmond`

* [OSINT] What is the name of the golf course that is near the registrant address for microsoft.com? `Bellevue Golf Course` by googling.

* What is the registered Tech Email for microsoft.com? `msnhst@microsoft.com`

# [Task 9] - Networking Tools : DIG

> When you visit a website in your web browser this all happens automatically, but we can also do it manually with a tool called dig . Like ping and traceroute, dig should be installed automatically on Linux systems.

> Dig allows us to manually query recursive DNS servers of our choice for information about domains:
dig <domain> @<dns-server-ip>

`Dig` is a very useful tool for network troubleshooting.

* What is DNS short for? `Domain Name System`

* What is the first type of DNS server your computer would query when you search for a domain? `Recursive`

* What type of DNS server contains records specific to domain extensions (i.e. .com, .co.uk, etc)? Use the long version of the name. `Top-Level Domain`

* Where is the very first place your computer would look to find the IP address of a domain? `Local cache`

* [Research] Google runs two public DNS servers. One of them can be queried with the IP 8.8.8.8, what is the IP address of the other one? `8.8.4.4` by googling.

* If a DNS query has a TTL of 24 hours, what number would the dig query show?  
In 24 hours, there are 60 * 60 * 24 = 86400 seconds.  
Therefore the dig will show the number `86400`.
