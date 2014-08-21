---
layout: post
title: "Announcing Stampede.io: A Hybrid IaaS/Docker Orchestation Platform Running on CoreOS"
date: 2014-08-21 16:54:52 -0700
comments: true
categories: 
---

{% youtube UsQ9cVLieaQ %}

I’d like to announce [Stampede.io][1].  Stampede is a hybrid IaaS/Docker orchestration platform running on CoreOS.  It’s extremely simple to get up and running and should take less than 10 minutes if you already have Fleet running or a fresh install through Vagrant.  There’s also [a short demo][2] that gives a good overview of the current functionality.  The main features at the moment are

* Virtual Machines
  * Libvirt/KVM
  * EC2/OpenStack images work out of the box
  * EC2 style meta data
  * OpenStack config drive
  * Managed DNS/DHCP
  * User data
  * Floating IPs
  * Private networking
  * VNC Console
  * CoreOS, Ubuntu, Fedora, and Cirros templates preconfigured
* Docker
  * Link containers across servers
  * Dynamically reassign links and ports
* Networking
  * VMs and containers can share the same network space
  * By default, a private IPSec VPN is created that spans servers
  * All containers and VMs live on a virtual network that can span across cloud
  * Can also use any libvirt networking models for VMs
* Interface
  * UI
  * REST API
    * Use web browser to explore and use API
  * Command line client
  * Python API bindings

While I feel Stampede is currently a pretty useful platform, I think the ideas behind the platform and what I’d like to accomplish are far more compelling.  On the surface this may appear to be similar to most IaaS or Docker orchestrations tools you’ve seen, but I assure you under the hood it’s implemented quite differently.  There’s many new ideas I’m playing around with, but there are two specific ideas I’d like to point out.  First is Orchestration as a Service and the second is hybrid IaaS/Container orchestration.  I talked about both these topics at more length in a [recent blog][3] I did.

## Orchestration as a Service

The basic idea behind Orchestration as a Service (OaaS) is to level the playing field and make it more feasible for smaller providers to compete in the cloud space.  AWS, GCE, and Azure are such juggernauts it’s hard to imagine another company would come around and enter the IaaS market, especially with margins perceived to be so low.  To compete with the big three, you have to operate at their scale.  On the other hand, you can get physical servers from just about anywhere and at a far cheaper price.  The premise of Stampede and Orchestration as a Service (OaaS) is that with a good amount of orchestration I could construct a cloud on par with AWS (ELB, EBS, VPC, etc) if all I start with is a pool of x86_64 servers that have an empty Linux distro (CoreOS), L3 connectivity, and additional block devices for storage.  By decoupling the physical infrastructure from the orchestration layer you enable the consumer to acquire hardware from whatever provider they choose.  I strongly believe this model could transform the cloud space, and make it far healthier than what it is today.  The only companies that can compete today are the ones that can afford to burn cash.

## Hybrid IaaS/Container Orchestration

I very much believe that containerization is the next big thing.  But, as [I spoke about before][3], I feel the current approach of Container/Docker orchestration tools will further cement the future of the current IaaS players.  In order to to make other clouds and especially bare metal more attractive, container orchestration tools need to take on more complex storage and networking orchestration.  Basically the same storage and networking orchestration seen in IaaS.  While many tout new application architectures will remove the need for reliable storage, or networking orchestration in general, the whole world will not rewrite their applications.  AWS is a great example of this.  When AWS launched it was ephemeral VMs only.  Not until customers demanded it did they add EBS and VPC.  While many may talk of architecting your application for the cloud, the real success of AWS was that they found technologies to helped move legacy, non-cloud architectures into the cloud.  With containerization that same practical route will be key to the widespread adoption of containerization.  While I very much like the newer architectures that are emerging, you can not expect everyone to rewrite their apps to be based on ephemeral storage and service discovery.

In the end I believe the same approaches and technologies used in IaaS orchestration are very applicable to Containers.  IaaS by itself is not sufficient for containers, and thus I’ve built a hybrid IaaS/Container orchestration system.

I’m very proud to show off this work, but it is still raw.  The intention is to demonstrate the feasibility of what could be accomplished.  Hopefully you'll find this work appealing.  Have fun!

Darren Shepherd - https://www.linkedin.com/in/darrensshepherd

  [1]: http://stampede.io
  [2]: http://youtu.be/UsQ9cVLieaQ
  [3]: http://www.ibuildthecloud.com/blog/2014/08/12/evolution-of-docker-and-its-impact-on-aws/
