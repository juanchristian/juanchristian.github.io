---
layout: post
title: Information exposure on EC-Council's Aspen site
---

If you are reading this, chances are you already know EC-Council and its online course platform, Aspen. But, for those who don't know, here is a little introduction directly from EC-Council's site:

> International Council of E-Commerce Consultants, also known as EC-Council, is the world's largest cyber security technical certification body. We operate in 145 countries globally and we are the owner and developer of the world-famous Certified Ethical Hacker (CEH), Computer Hacking Forensics Investigator (CHFI), Certified Security Analyst (ECSA), License Penetration Testing (Practical) programs, among others.

As a Certified Ethical Hacker (CEH) and a Certified EC-Council Instructor (CEI), I use the Aspen site occasionally. During one of my visits I needed to download all CEHv9 files in one go, instead of manually downloading. The download URL was pretty straightforward: `https://aspen.eccouncil.org/Training/EbookDownload?ebookFormat=Lock%20Lizard&ModuleId=487`

Where `487` is the ID of the file to download, in this case the downloaded file was "CEHv9 Module 00.pdc".

You may think the ID is incremental and to download the next module you just need to increment it by one, and you would be correct. Basically, all CEHv9 modules, from 00 to 18, are contained in the ID range 487–504. No problem at all here, I was logged in and had the CEHv9 course in my account, so it's expected that I could download all the files.

But, things got interesting when I continued to increment/decrement the ID to see what I would get, the video below answers that question.

<video controls>
  <source src="/resources/posts/2020-03-21-information-exposure-on-ec-councils-aspen-site/PoC.mp4" type="video/mp4">
  Your browser does not support HTML5 video.
</video>

As you can see in the video, I created a new account that wasn't registered in any course, but could download files freely, including materials from CEHv10, ECSAv10 and CSCUv2 for example. There were unencrypted videos, but most of the files were PDC (PDF file encrypted with Lizard Safeguard), basically a PDF with DRM. So, even if I could download them I wouldn't be able to read without breaking the DRM (breaking DRM is out of the scope of this report), but at least, as an attacker, I would be one step closer to my objective.

That's why defense-in-depth (also known as layered security) is something essential. The application layer failed, but in the end, DRM prevented further damages at data layer. The site didn't enforce proper authorization, so anyone could download everything. Under CWE, this is an example of [CWE-200: Exposure of Sensitive Information to an Unauthorized Actor](https://cwe.mitre.org/data/definitions/200.html){:target="_blank"}.

I reported this vulnerability to EC-Council on 2019–11–01, they took a few weeks to fix it, but only recently allowed me to disclose it. If you are reading this, you won't be able to download the entire EC-Council library anymore. You would be presented with the message below, if you tried to download a file you weren't supposed to.

![Authorization working as expected](/resources/posts/2020-03-21-information-exposure-on-ec-councils-aspen-site/img1.png "Authorization working as expected")

This is another example of a security-related company who commited a simple, yet potentially dangerous mistake. In the past I [wrote about]({{ site.url }}{% post_url 2019-05-24-user-enumeration-on-qualys-training-and-certification-site %}){:target="_blank"} Qualys and the user enumaration in its traning & certification site. It's always good to remember: don't take security lightly, even the "experts" fail from time to time, so can you.