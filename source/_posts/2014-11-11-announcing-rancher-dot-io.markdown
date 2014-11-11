---
layout: post
title: "Announcing Rancher.io: Portable Infrastructure Services for Docker"
date: 2014-11-11 00:21:28 -0700
comments: true
categories: 
---

Almost one year ago I started [Stampede](http://stampede.io) as an R&D project to look at the implications of Docker on cloud computing moving forward, and as such I’ve explored many ideas.  After releasing Stampede, and getting so much great feedback, I've decided to concentrate my efforts.  I’m renaming Stampede.io to [Rancher.io](http://rancher.io) to signify the new direction and focus the project is taking.  Going forward, instead of the experimental personal project that Stampede was, Rancher will be a well-sponsored open source project focused on building a portable implementation of infrastructure services similar to EBS, VPC, ELB, and many other services.

Most Docker projects today look to build solutions that will sit on top of Docker and allow developers to schedule, monitor and manage applications.  Rancher takes a different approach, it focuses on developing infrastructure services that will sit below Docker.  Rancher will deliver a completely portable implementation of the infrastructure services you would expect to find in a cloud such as AWS, including EBS, VPC, ELB, Security Groups, Monitoring, RDS, and many more.

Docker has dramatically impacted cloud computing because it offers a portable package for an application.  This portability means an application will run on any infrastructure whether it is your laptop, a physical server, or a cloud.  Once you have a portable application you can do some amazing things to improve application performance, availability and costs using scheduling, service discovery, application templating, policy management, etc.  Exciting projects including Kubernetes, Panamax, Helios, Clocker, Dies, etc, are building technology on top of Docker to deliver this type of value.

Rancher focuses on a very different problem.  Imagine I have an application running on AWS today that uses functionality from EBS and VPC.  If I Dockerize my application and run it on AWS, I will still be able to leverage EBS and VPC.  However, if I move that application to Digital Ocean, or my own datacenter, those services just don’t exist.  While Docker itself is portable, infrastructure services vary dramatically between clouds, and data centers, making real application portability almost impossible without architecting around those differences in your application.  Rancher focuses on building portable implementations of these infrastructure services that can run on any cloud, or even multiple clouds at the same time.  With Rancher you will be able to get infrastructure services as reliable as AWS provides, anywhere, including on your own hardware, another cloud provider, a dedicated server provider, or any combination of physical and virtual resources.  With Rancher, hybrid cloud is no longer an over-hyped marketing term that relies on trying to make incompatible APIs work together,  but instead a core capability as ubiquitous as Linux and Docker.

In the short term you can expect Rancher to focus on fundamental storage and networking services similar to EBS, VPC, ELB, and Route 53.  Once those fundamental services are implemented they will serve as the foundation for other infrastructure services similar to CloudWatch, CloudMetrics, AutoScaling, RDS etc.

I’m building Rancher, because I want users to be able to access awesome portable infrastructure services everywhere they can run Docker.  Docker is portable because Linux is everywhere, and Rancher takes the same approach; we build storage, networking, and other infrastructure services from simple Linux VMs and servers. Thank you again for all of the input on Stampede, and I hope you will join me in making Rancher an enormous success. 

