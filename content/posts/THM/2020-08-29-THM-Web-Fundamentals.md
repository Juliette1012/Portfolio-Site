---
layout: post
title: Write-Up [THM] Web Fundamentals
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Web, Http]
featured-image:  thm/web-fundamentals/theme.png
featured-image-alt: Web Fundamentals
---

It's a write-up about the room : [Try Hack Me - Room : Web Fundamentals](https://tryhackme.com/room/webfundamentals)

# [Task 1] Introduction and objectives

> This room is designed as a basic intro to how the web works.

> We'll cover HTTP requests and responses, web servers, cookies and then put them all to use in a mini Capture the Flag at the end.

# [Task 2] How do we load websites ?

* What request verb is used to retrieve page content? `GET`

* What port do web servers normally listen on ? `80`

* What's responsible for making websites look fancy? `css`

# [Task 3] More Http : Verbs and request format

![Requests](/assets/img/thm/web-fundamentals/requests.png)

* What verb would be used for a login? `POST`

* What verb would be used to see your bank balance once you're logged in? `GET`

* Does the body of a GET request matter? Yea/Nay `Nay` 

![Responses](/assets/img/thm/web-fundamentals/responses.png)

* What's the status code for "I'm a teapot"? `418` 

We used this website : [mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) to find the answer.

* What status code will you get if you need to authenticate to access some content, and you're unauthenticated? `401`

# [Task 4] Cookies, tasty !

![Cookies](/assets/img/thm/web-fundamentals/cookies.png)

# [Task 5] Mini CTF

> There's a web server running on `http://MACHINE_IP:8081`. Connect to it and get the flags!

```
    GET request. Make a GET request to the web server with path /ctf/get
    POST request. Make a POST request with the body "flag_please" to /ctf/post
    Get a cookie. Make a GET request to /ctf/getcookie and check the cookie the server gives you
    Set a cookie. Set a cookie with name "flagpls" and value "flagpls" in your devtools and make a GET request to /ctf/sendcookie
```

* What's the GET flag?

We use : `curl --request GET http://10.10.222.121:8081/ctf/get` and find **thm{162520bec925bd7979e9ae65a725f99f}**.

* What's the POST flag? 

We use : `curl --request POST --data "flag_please"  http://10.10.222.121:8081/ctf/post` and find **thm{3517c902e22def9c6e09b99a9040ba09}**.

* What's the "Get a cookie" flag? 

We use : `curl --request GET -c cookielist. http://10.10.222.121:8081/ctf/getcookie` and find **thm{91b1ac2606f36b935f465558213d7ebd}**.

* What's the "Set a cookie" flag?

We use : `curl --cookie flagpls=flagpls http://10.10.222.121:8081/ctf/sendcookie` and find **thm{c10b5cb7546f359d19c747db2d0f47b3}**.