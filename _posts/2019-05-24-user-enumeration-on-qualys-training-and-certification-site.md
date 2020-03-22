---
layout: post
title: User enumeration on Qualys Training & Certification site
---

First of all, let's clarify what is user enumeration. In simple terms, user enumeration is the action of listing the users of a system or application. It's a vulnerability on the confidentiality of the system/application. It's included in A2 Weak authentication and session management from OWASP Top 10. It's also covered in the OWASP Testing Guide, specifically the item Testing for Account Enumeration and Guessable User Account (OTG-IDENT-004).

Now, talking about the [Qualys Training & Certification](https://www.qualys.com/training/){:target="_blank"} user enumeration case. The site offers a bunch of great online courses that I was interested in, so logically I signed up. Just the other day, I forgot my password so I had to resort to the good old "forgot my password" feature. That's when I spotted something interesting: a user enumeration possibility.

![Bad response!](/resources/posts/2019-05-24-user-enumeration-on-qualys-training-and-certification-site/img1.png "Bad response!")

This is somewhat dangerous as the site requires you to sign up with an enterprise or educational email. Threat actors could infer that your company is using, or planing to use, Qualys solutions because one or more employe emails (e.g. the security team) were registered in the site. Even if you didn’t use an enterprise email, instead, you used your .edu email, it’s also unfortunate to have it exposed that way.

It’s worth noticing in the image the text “© 2019 SumTotal”, which indicates that Qualys uses the SumTotal Learning Management system, a third-party LMS solution.

After discovering it, I ethically reported the vulnerability to Qualys before making it public, and they had the vendor fix it by the time of this post. Nowadays anyone that uses the "forgot my password" feature will be presented with the screen below that doesn't give any sensitive information.

![Good response!](/resources/posts/2019-05-24-user-enumeration-on-qualys-training-and-certification-site/img2.png "Good response!")

What we learned with that? Even big guys like Qualys, whose core business is vulnerability, can make simple mistakes from time to time, so it's always good to continuously audit and enhance the security of your environment and also pay close attention to vendor solutions that your company uses, as they can also be exploited by threat actors.

Update #1: You can read Qualys's official statement [here](https://blog.qualys.com/securitylabs/2019/06/01/third-party-user-enumeration-issue-resolved){:target="_blank"}.
