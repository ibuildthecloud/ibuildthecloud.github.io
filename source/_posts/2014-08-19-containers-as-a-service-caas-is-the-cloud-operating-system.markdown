---
layout: post
title: "Containers as a Service (CaaS) is the Cloud Operating System"
date: 2014-08-19 13:18:46 -0700
comments: true
categories: 
---

Historically, the architecture of PaaS and IaaS has been that PaaS sits on top of IaaS.  As containers have emerged as a first class technology, there seems to be a new intermediate layer forming.  With the rise of Docker, I’ve observed two classes of platforms being built: PaaS “powered by Docker,” and Docker orchestration.  A better PaaS powered by Docker is personally of very little interest to me as it’s just a better iteration of what has been done in the past.  Docker orchestration has the potential to be more transformative.  It’s Docker orchestration that has introduced this new layer I mentioned.  Many have coined this as Containers as a Service (CaaS).  As I’ve sat and pondered the real value and impact of this layer, it finally dawned on me that CaaS is in fact the “The Cloud Operating System” and Docker’s role is to define it’s interface.

## The IaaS/PaaS dichotomy

With IaaS you get raw assets that are extremely flexible.  With PaaS you get a very locked down experience that is optimized for a particular use case.  These two solution are very much on opposite sides of the spectrum.

Netflix serves as probably the best example of someone fully exploiting the capabilities of the cloud.  What they have done with AWS is truly amazing and shows what could be accomplished.  They also serve as a cautionary tale.  While they’ve fully exploited the cloud, when I last looked, Netflix has released over 35 open source projects all centered on running scalable applications in the cloud.  While most people are not trying to run at the scale of Netflix, it does point out that there is still a significant amount of tooling needed to run in the cloud.  IaaS gives you raw infrastructure on demand but you still need to manage that infrastructure in some fashion.

For those wanting to avoid the overhead of maintaining servers, operating systems, and runtimes, PaaS has historically been presented as the solution.  PaaS is great in that you can just focus on your code and not worry about all the runtime maintenance.  Quickly though, you run into restrictions on what your code can do.  For example, running Java on Google AppEngine (GAE) you often need to first check and see if the third party libraries you are using are compatible with GAE as not all of the JRE is fully exposed.  Other functionality, like listening on sockets, is just not possible.  

## Introduction of Containers as a Service (CaaS)

The introduction of CaaS solves a lot of practical issues with the IaaS/PaaS dichotomy and additionally further expands the capabilities of what one can do.  CaaS really serves as the missing layer into between IaaS and PaaS.  When you look at a server, you can break it into three logical layers: physical hardware, operating system, and applications.  Respectively, you can look at that as IaaS, CaaS, and PaaS.

IaaS provides hardware assets whether it’s physical or a virtual representation of the physical counterpart.  What you really get are RAM, CPUs, hard drives, and NICs.  You, as the consumer of IaaS, are in control of everything else.  While the cloud provider may supply a template with an operating system, the consumer is still ultimately responsible for it.

PaaS provides an application runtime.  This ends up being language specific, so what PaaS is providing is a managed environment for Java, Ruby, Python, etc.  PaaS is really concerned about providing what runs inside the process.

What if I just want a generic framework to run processes of any size or shape.  That is the focus of CaaS.  While IaaS provides the hardware and PaaS provides the runtime in the process, CaaS is the missing layer that glues these two things together.  

## The Cloud Operating System

CaaS plays the role of the operating system.  Wikipedia states, “An operating system (OS) is software that manages computer hardware and software resources and provides common services for computer programs.”  CaaS’s responsibility is to provide a platform in which you can run processes and manage the services and resources needed by those processes.  What runs inside the process is completely arbitrary to CaaS.

CaaS really is the next logical evolution after IaaS.  Now that I have hardware on demand, I no longer want to manage an operating system.  Instead I’d like to focus on my application, without the constraints that PaaS imposes.  There still is a value to PaaS, but its scope is diminished to providing a managed runtime.  In fact, with CaaS it is significantly easier to build PaaS.

Many projects in the past have taken on the moniker of “The Cloud Operating System.”  I’ve never particularly liked that as I didn’t feel there was any real definition of what that meant.  Instead it was just a marketing term just as useless as the term “Cloud.”  Finally, with CaaS, I think the “Cloud Operating System” is a correct fit.  CaaS is your operating system.

## The Role of Docker

How does Docker fit into all this?  As Solomon Hykes, CTO of Docker, said, “The real value of Docker is not technology.  It’s getting people to agree on something.”  If CaaS provides the operating system, and the consumer provides the user space, what is the interface of that operating system?  In the UNIX world we have POSIX.  Love it or hate it, it is a standard that defines an interface to the operating system.  Docker largely fills a similar role.

Docker provides the language in how we describe and talk about containers.  It also defines what basic storage, networking, and services are available to the containers.  Furthermore, it helps to ensure that applications written for Docker stay portable across varying types of infrastructure.

In summary, CaaS is the Cloud Operating System and Docker serves as its portable interface.
