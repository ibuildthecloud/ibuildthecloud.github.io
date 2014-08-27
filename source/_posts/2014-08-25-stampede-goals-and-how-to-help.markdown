---
layout: post
title: "Stampede: How You Can Help"
date: 2014-08-27 09:24:28 -0700
comments: true
categories: 
---

The response to the initial release of Stampede has been overwhelmingly positive and I thank everyone for their nice comments.  I've had many questions regarding how people can help.  The biggest help at this point would be feedback.  Stampede has been my pet project for a couple months and it has served as a way for me to validate some ideas I've had.  How and if I continue forward with this work all depends on whether other people think this would be a useful platform.  What would be helpful is for people to think about what's missing from this platform that would prevent them from using it as something to manage their production apps.  Don't think about new greenfield applications but instead your current production apps that have some warts and hacks.  If you were to Docker-ize those apps, what would Stampede really need to manage those in production?  For example, my current roadmap would be to implement the following features:

* Fully managed volumes (Docker and KVM) with snapshot, restore, and backup to S3
* Load balancing
* Security groups

What other features would you need?  Think about bare metal too.  For apps running on AWS, if you were to Docker-ize it and run it on bare metal.  What features would you lack because you no longer have EC2.

Stampede, in its current form, has big functionality gaps and is not production worthy.  But this code base is not something I just hacked together.  My background is in writing these orchestration systems and many of the ideas I wanted to validate were about how to write a better orchestration platform and not at all related to specific virtualization/container technology.  Out of the ~50k lines of code I wrote more that 90% of that is just framework.  There is actually very little code that has to do with Docker/KVM.  The point I'm trying to make is that I feel this is a strong platform and I have only scratched the surface of what it can do.

Please tell your friends about Stampede, run it yourself, let me know the gaps and how you would use it.  Once I get an idea of people's interests then I can better decide how to take this platform forward.  [Contact Information](https://github.com/cattleio/stampede#contact)
