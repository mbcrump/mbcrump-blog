---
layout: post
title: "Azure Tips and Tricks Part 53 - Prebuilt Azure VMs ready for Containers"
excerpt: "Learn how to use prebuilt azure vms with containers"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Prebuilt Azure VMs ready for Containers

While I was at Microsoft Connect last week, I met someone who recently read my Docker Container mini-series that covered [Getting Started with Docker and Azure](http://www.michaelcrump.net/azure-tips-and-tricks45/), [Running an app inside a Container Image with Docker](http://www.michaelcrump.net/azure-tips-and-tricks46/), [Creating a Container Image with Docker](http://www.michaelcrump.net/azure-tips-and-tricks47/) and [Pushing a Container Image to a Docker Repo](http://www.michaelcrump.net/azure-tips-and-tricks48/). The question that came up was how they wish we had prebuilt Azure VMs that had container images already on them. This would save them additional time and something that they would expect. You can imagine their surprise when I told them that we had them already. In this post, we'll take a quick look at how to find them. 

Open **Virtual Machines** and click on **Add**, then search for **containers**. You may optionally want to set a filter to restrict to Windows and Linux based. 

<img style="border:3px solid #021a40" src="/files/vmcontainer2.png">

<img style="border:3px solid #021a40" src="/files/vmcontainer1.png">

From this screen, you can see a variety of Windows and Linux VMs. If I wanted a Windows VM, then I'd probably pick this one: 

<img style="border:3px solid #021a40" src="/files/vmcontainer3.png">

Note the following text: It includes Windows Server container images installed and ready to use with Docker.

For Linux, I might choose this one:

<img style="border:3px solid #021a40" src="/files/vmcontainer4.png">

Note the following text: When we started the RancherOS project, we set out to build a minimalist Linux distribution that was perfect for running Docker containers. We wanted to run Docker directly on top of the Linux Kernel, and have all user-space Linux services be distributed as Docker containers.

Of course, there are a lot of options out there, so pick what is best for you! This will just help you get up and running even faster.

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 