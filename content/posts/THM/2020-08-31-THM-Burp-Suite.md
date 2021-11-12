---
title: Write-Up [THM] Burp Suite
template: "post"
date: "2020-08-28"
draft: false
category: "Write-Ups, TryHackMe"
tags:
  - "TryHackMe"
  - "Burp Suite"
  - "Web"
social-image: "/media/thm/burp-suite/theme.png"
description: "It's a write-up about the room : [Try Hack Me - Room : Burp Suite](https://tryhackme.com/room/rpburpsuite)"
---

It's a write-up about the room : [Try Hack Me - Room : Burp Suite](https://tryhackme.com/room/rpburpsuite)

# [Task 1] Intro

![Task 1](/media/thm/burp-suite/task-1.png)

# [Task 2] Installation

We install Burp Suite.

# [Task 3] Gettin' [CA] Certified 

> Before we can start using our new installation (or preinstalled) Burp Suite, we'll have to fix a certificate warning. We need to install a CA certificate as BurpSuite acts as a proxy between your browser and sending it through the internet - It allows the BurpSuite Application to read and send on HTTPS data. 

# [Task 4] - Overview of Features

* Which tool in Burp Suite can we use to perform a 'diff' on responses and other pieces of data? `Comparer`

* What tool could we use to analyze randomness in different pieces of data such as password reset tokens? `Sequencer`

* What tool could we use to analyze randomness in different pieces of data such as password reset tokens? `Target`

* While only available in the premium versions of Burp Suite, which tool can we use to automatically identify different vulnerabilities in the application we are examining? `Scanner`

*  	Encoding or decoding data can be particularly useful when examining URL parameters or protections on a form, which tool allows us to do just that? `Decoder`

* Which tool allows us to redirect our web traffic into Burp for further examination? `Proxy`

* Simple in concept but powerful in execution, which tool allows us to reissue requests? `Repeater`

* With four modes, which tool in Burp can we use for a variety of purposes such as field fuzzing? `Intruder`

* Last but certainly not least, which tool allows us to modify Burp Suite via the addition of extensions? `Extender`

# [Task 5] Engage Dark Mode

> With Burp Suite launched, let's first navigate to the 'User options' tab. 
> Next, click on the 'Display' sub-tab.
> Now, click on the 'Look and feel' drop-down menu. Select 'Darcula'.  
> Finally, close and relaunch Burp Suite to have dark theme (or whichever theme you picked) take effect.

# [Task 6] - Proxy

![Task 6](/media/thm/burp-suite/task-6.png)

* By default, the Burp Suite proxy listens on only one interface. What is it? Use the format of IP:PORT `127.0.0.1:8080`

* Return to your web browser and navigate to the web application hosted on the VM we deployed just a bit ago. Note that the page appears to be continuously loading. Change back to Burp Suite, we now have a request that's waiting in our intercept tab. Take a look at the actions, which shortcut allows us to forward the request to Repeater? `CTRL-R`

* How about if we wanted to forward our request to Intruder? `CTRL-I`

* Burp Suite saves the history of requests sent through the proxy along with their varying details. This can be especially useful when we need to have proof of our actions throughout a penetration test or we want to modify and resend a request we sent a while back. What is the name of the first section wherein general web requests (GET/POST) are saved? `HTTP history`

* Defined in RFC 6455 as a low-latency communication protocol that doesn't require HTTP encapsulation, what is the name of the second section of our saved history in Burp Suite? These are commonly used in collaborate application which require real-time updates (Google Docs is an excellent example here). `WebSockets history`

* Before we move onto exploring our target definition, let's take a look at some of the advanced customization we can utilize in the Burp proxy. Move over to the Options section of the Proxy tab and scroll down to Intercept Client Requests. Here we can apply further fine-grained rules to define which requests we would like to intercept. Perhaps the most useful out of the default rules is our only AND rule. What is it's match type? `URL`

* How about it's 'Relationship'? In this situation, enabling this match rule can be incredibly useful following target definition as we can effectively leave intercept on permanently (unless we need to navigate without intercept) as it won't disturb sites which are outside of our scope - something which is particularly nice if we need to Google something in the same browser. `Is in target scope`

# [Task 7] - Target Definition

![Task 7](/media/thm/burp-suite/task-7.png)

* Browse around the rest of the application to build out our page structure in the target tab. Once you've visited most of the pages of the site return to Burp Suite and expand the various levels of the application directory. What do we call this representation of the collective web application? `site map`

* What is the term for browsing the application as a normal user prior to examining it further? `happy path`

* The issue definitions found here are how Burp Suite defines issues within reporting. While getting started, these issue definitions can be particularly helpful for understanding and categorizing various findings we might have. Which poisoning issue arises when an application behind a cache process input that is not included in the cache key? `Web cache poisoning`

# [Task 8] - Puttin' it on Repeat[er]

![Task 8](/media/thm/burp-suite/task-8.png)

* Try logging in with invalid credentials. What error is generated when login fails? `Invalid email or password`

* Now that we've sent the request to Repeater, let's try adjusting the request such that we are sending a single quote (') as both the email and password. What error is generated from this request? `SQLITE_ERROR`

* What field do we have to modify in order to submit a zero-star review? `rating`

# [Task 9] - Help ! There's an Intruder !

![Task 9](/media/thm/burp-suite/task-9.png)

* Which attack type allows us to select multiple payload sets (one per position) and iterate through them simultaneously? `Pitchfork`

* How about the attack type which allows us to use one payload set in every single position we've selected simultaneously? `Battering Ram`

* Which attack type allows us to select multiple payload sets (one per position) and iterate through all possible combinations? `Cluster Bomb`

* Perhaps the most commonly used, which attack type allows us to cycle through our payload set, putting the next available payload in each position in turn? `Sniper`

* Finally, click 'Start attack'. What is the first payload that returns a 200 status code, showing that we have successfully bypassed authentication? `a' or 1=1--`

# [Task 10] - As it turns out the machines are better at math than us

> Burp's Sequencer, per the Burp documentation, is a tool for analyzing the quality of randomness in an application's sessions tokens and other important data items that are otherwise intended to be unpredictable. Some commonly analyzed items include:

- Session tokens
- Anti-CSRF (Cross-Site Request Forgery) tokens
- Password reset tokens (sent with password resets that in theory uniquely tie users with their password reset requests)

* Parse through the results. What is the effective estimated entropy measured in? `bits`

* In order to find the usable bits of entropy we often have to make some adjustments to have a normalized dataset. What item is converted in this process? `token`

# [Task 11] - Decoder and Comparer

> Decoder and Comparer, while lesser tools within Burp Suite, are still essential to understand and leverage as part of being a proficient web app tester. 

> As the name suggests, Decoder is a tool that allows us to perform various transforms on pieces of data. These transforms vary from decoding/encoding to various bases or URL encoding. We chain these transforms together and Decoder will automatically spawn an additional tier each time we select a decoder, encoder, or hash. This tool ultimately functions very similarly to CyberChef, albeit slightly less powerful.

* What character does the %20 in the request we copied into Decoder decode as? `Space`

* Similar to CyberChef, Decoder also has a 'Magic' mode where it will automatically attempt to decode the input it is provided. What is this mode called? `Smart Decode`

* What can we load into Comparer to see differences in what various user roles can access? This is very useful to check for access control issues. `site maps`

* Comparer can perform a diff against two different metrics, which one allows us to examine the data loaded in as-is rather than breaking it down into bytes? `words`

# [Task 12] - Installing some Mods [Extender]

![Task 12](/media/thm/burp-suite/task-12.png)

* Which extension allows us too bookmark various requests? `Boorkmarks`

# [Task 13] - But wait, there's more ! 

* Download the report attached to this task. What is the only critical issue? `Cross-origin resource sharing: arbitrary origin trusted`

* How many 'Certain' low issues did Burp find? `12`
