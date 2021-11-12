---
layout: post
title: Write-Up [THM] Google Dorking
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Google]
featured-image:  thm/google-dorking/theme.png
featured-image-alt: Google Dorking
---

It's a write-up about the room : [Try Hack Me - Room : Google Dorking](https://tryhackme.com/room/googledorking)

# [Task 1] Introduction

![Task 1](/assets/img/thm/google-dorking/task-1.png)

# [Task 2] Let's Learn About Crawlers

![Crawler](/assets/img/thm/google-dorking/crawler.png)

> In the diagram above, the `crawler` initially finds “mywebsite.com”, where it crawls the contents of the website - finding the same keywords (“Apple", “Banana” and “Pear”) as before, but it has additionally found an external URL. Once the crawler is complete on “mywebsite.com”, it'll proceed to crawl the contents of the website “anotherwebsite.com”, where the `keywords` ("Tomatoes", “Strawberries” and “Pineapples”) are found on it. The crawler's dictionary now contains the contents of both “mywebsite.com” and “anotherwebsite.com”, which is then stored and saved within the search engine.

![Answer task 2](/assets/img/thm/google-dorking/answer-2.png)

# [Task 3] Enter: Search Engine Optimisation

> At an abstract view, search engines will `prioritise` those domains that are easier to index. There are many factors in how “optimal” a domain is - resulting in something similar to a point-scoring system.

[SEO Site Checkup](https://seositecheckup.com) is a website which enables to check the rating of websites.

We use this one, to answer the different questions below : 

![Answer task 3](/assets/img/thm/google-dorking/answer-3.png)

# [Task 4] Beepboop - Robots.txt

`Robots.txt` is the first file indexed by `crawlers` when visiting a website.  

This file must be served at the root directory and indicate whether certain user agents (web-crawling software) can or cannot crawl parts of a website.  

Thse crawl instructions are specified by `disallowing` or `allowing`the behavior of certain (or all) user agents.

Robots.txt is similar to `Sitemaps`. This one is located at `http://mywebsite.com/sitemap.xml`. 

![Answer task 4](/assets/img/thm/google-dorking/answer-4.png)

# [Task 5] Sitemaps

> `Sitemaps` are indicative resources that are helpful for crawlers, as they specify the necessary routes to find content on the domain. The below illustration is a good example of the structure of a website, and how it may look on a "Sitemap":

![Sitemaps](/assets/img/thm/google-dorking/sitemaps.png)

**The easier a website is to `Crawl`, the more optimised it is for the `Search Engine`.**

![Answer task 5](/assets/img/thm/google-dorking/answer-5.png)

# [Task 6] What is Google Dorking ?

Now to the meat of the whole `Google Dorking`/Google Fu by using the index categorizations for websearches that Google has meticulously gathered. 

All those crawlers can now be used in reverse uno fashion for your speedy research !

![Answer task 6](/assets/img/thm/google-dorking/answer-6.png)