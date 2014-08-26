---
layout: post
title: "Stampede: Goals and How to Help"
date: 2014-08-25 09:24:28 -0700
comments: true
categories: 
---

The response to the initial release of Stampede has been overwhelmingly positive and I thank everyone for their nice comments.  I've had many questions regarding the goals of Stampede and how people can help.

# Goals

The overarching goal of Stampede is really to just make private cloud simple and accessible to most people.  The vast majority of private clouds are less than 50-100 servers.  For that size of an installation, private cloud is really quite simple.  You don't even really hit most scaling issues.  If you already have the skill set to run, monitor, and manage that many Linux servers, running a private cloud should be a no brainer.  But currently it's not, it's just too difficult.  Furthermore, most clouds are used for dev/test.  Dev/test environments usually don't need the operational excellence production demands.  This should make cloud even easier, but again, it's not.

For clouds that go above 100 servers it does get more complex.  Stampede is designed to handle these complexities and a single management is designed to scale to 100k hosts.  For clouds of this size it is more difficult and the complexity will increase.  The complexity of scale should be O(log n), currently it seems to be more like O(n^2).

# How you can help

The main thing you can do to help is give feedback.  Install Stampede and try it out.  It's not production quality yet and it doesn't have all the features it should.  I want to create a platform you want to run.  Tell me what sucks, what's a pain.  Take some time and think if you were to really use this in production, what you would need.

I have no delusions that I alone can create a platform to rival the feature set of the current stacks out there.  And I really don't want to.  It's incredibly complex to come up with a solution that handles everyones requirements.  The goal is to instead tackle the 80% that everyone needs and then provide simple hooks for the rest.  If you want PCI passthrough I don't want to build a whole framework to manage PCI devices.  Instead I'll let you know how you can easily add some attributes to the API and then create some scripts on the backend to manage it.  We already have the Apache HTTPD of IaaS stacks, let's build Nginx now.

I look forward to your feedback. [Contact me](https://github.com/cattleio/stampede#contact) or just open a [GitHub issue](https://github.com/cattleio/stampede/issues).
