---
layout: post
title: "Is Docker Fundamentally Flawed?"
date: 2014-12-03 16:34:41 -0700
comments: true
categories:
---

When [Rocket was announced](https://coreos.com/blog/rocket/) CoreOS stated

> From a security and composability perspective, the Docker process model - where everything runs through a central daemon - is fundamentally flawed.

I wanted to give a bit more context that may help users understand why CoreOS might feel so strongly that Docker is fundamentally flawed.  ...And surprisingly this has a lot to do with systemd.

When systemd starts a service it creates a series of cgroups.  As the service spawns child processes, the children by default stay in the same cgroup.  This is the way systemd always knows which processes are associated with a service and additionally what resources they can consume.  If a service dies systemd can cleanup all processes associated with the service regardless of who is the parent.  This is really a clever design.

Now here's the problem, Docker breaks all of this (not intentionally).  When you do `docker run`, Docker makes a RPC call to the Docker daemon which spawns a child process that becomes the PID 1 of the container.  If your service unit contains a `docker run` command systemd will monitor the Docker client process.  As soon as the Docker client makes that RPC call systemd loses track of what is going on.  This is due to the fact that the container is spawned in a different cgroup from the Docker client that is being monitored by systemd.  In the end systemd can not manage Docker containers because of the daemon.  So you can begin to see why CoreOS would say that it is fundamentally flawed.

What would CoreOS want to see Docker do differently?  CoreOS would like Docker to remove the daemon such that containers are spawned as a child of the Docker client.  If Docker was to launch containers as a child then systemd would be able to effectively
manage Docker.  Again, you can see why CoreOS says it’s fundamentally flawed.

So why doesn't Docker change?  Why doesn't Docker just get rid of the daemon as it so clearly conflicts with systemd.  Well first you have to consider what the daemon does.  The daemon has several roles.  It provides the remote API, maintains the state of containers, sets up resources (like staging images), and then does the execution and cleanup of containers.  Rocket has no standalone daemon so how does it achieve all of this?  Rocket largely handles setting up the resources for the container (such as staging the image) and then delegates everything to systemd-nspawn to do the rest.

There’s the magic, systemd.  It's not that Rocket doesn't have a stand alone daemon it is just that that daemon happens to be systemd, PID 1, which runs as root.  So is Docker fundamentally flawed?  I can't imagine how you could say that because Rocket follow a very similar paradigm, it just happens to be built into systemd.  The fundamental issue is that both Docker and systemd want to be the daemon to manage containers.

This conflict ends up being the crux of the issue.  While CoreOS is touted as being the best platform to run docker, you have to realize that CoreOS revolves around systemd, not Docker.   Fleet, CoreOS’s container scheduler, in fact interfaces with systemd, not Docker.  It is merely a systemd unit scheduler and those units may just happen to run Docker containers.  As I mentioned before this model does not work well because systemd can not effectively manage Docker containers.  If you want to understand some more nitty-gritty details about this refer to a project I created, [systemd-docker](https://github.com/ibuildthecloud/systemd-docker), which was created as an attempt to find a happy compromise between systemd and Docker.

While CoreOS may list many reasons why Rocket is better, it also happens to be a nice opportunity to allow them to write a systemd friendly container system.  In fact if you want to build a Rocket stage1 implementation that is not built on systemd, you will most likely find yourself back to a design very similar to what Docker is today.

How can this be resolved?
-------------------------

I like CoreOS very much.  The sad truth is that running Docker containers on CoreOS is really not a nice experience.  I've spent a huge amount of time dealing with this and attempting to facilitate some solution.  We absolutely don't need a rewrite of Docker to fix all of this but we do need some cooperation.

There are two solutions for this problem.  First, it must be clear to say that Docker will not give up its daemon.  It is just not feasible because Docker would have to give up its remote API and then also be tied to systemd.  So the question becomes how can these two daemons (Docker and systemd) nicely cooperate.

One solution is that systemd exposes an API such that a caller can put a process into an existing cgroup or a child of a cgroup.  One of the main issues is that the Docker daemon has no ability to launch a container that is related to an existing systemd service unit.  I've [brought this up with the systemd developers](http://lists.freedesktop.org/archives/systemd-devel/2014-October/023944.html) and they have added it to their todo list.

The second solution is that the Docker daemon communicates back to the Docker client to launch the container as a child of the client and not the daemon.  I have had a couple discussions with Michael Crosby from Docker, Inc. on this topic that initiated from a [long IRC discussion](https://botbot.me/freenode/docker-dev/2014-07-10/?msg=17771621&page=7).  In the end it is a workable solution that can solve some other issues like Docker restarts not restarting containers.

There needs to be a change in systemd or Docker to fix this.  Why hasn't anything been done?  Simply put, nobody seems to be sufficiently motivated to do the work to fix the issue (including me).  Is Docker fundamentally flawed?  I don’t think so.
