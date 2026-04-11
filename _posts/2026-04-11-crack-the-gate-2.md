---
title: PicoCTF - Crack the Gate 2 Write-up
date: 2026-04-11 15:00:00 +0300
categories: [CTF Writeups, PicoCTF]
tags: [web-exploitation, burp-suite, brute-force, picoctf]
---

This is a medium-difficulty web exploitation challenge from PicoCTF. 

The description for this challenge is shown in the image below:

![Challenge Description](/assets/img/posts/Crack_the_Gate_2/description.png)

The hints provided for this challenge are:
1. What IP does the server think you’re coming from?
2. Read more about `X-Forwarded-For`.
3. You can rotate fake IPs to bypass rate limits.

The first thing I considered was that I already had the target email. Upon starting the instance, I was provided with a list of passwords. Therefore, I opened Burp Suite and intercepted the login request.

The second hint suggested reading more about the `X-Forwarded-For` header. This header is commonly used to spoof the origin IP address, tricking the web application into believing the request is coming from a trusted internal source. In most cases, we set this value to `127.0.0.1` (localhost).

![Burp Suite Request](/assets/img/posts/Crack_the_Gate_2/request.png)

Next, I sent the intercepted request to Burp Suite's **Intruder**. I loaded the provided password list as a payload and set the payload marker (`§`) on the password parameter to brute-force the login.

![Burp Suite Intruder](/assets/img/posts/Crack_the_Gate_2/intruder.png)

And just like that, we got the flag! 🚩

*Note: The last screenshot is from a different attempt because I forgot to capture it the first time. The correct password changes every time you spin up a new instance.*

I hope you found this write-up helpful! :)
