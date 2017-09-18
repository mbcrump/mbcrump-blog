---
layout: post
title: "Azure Tips and Tricks Part 15 - Underlying Software in Azure Cloud Shell"
excerpt: "Learn about some of the software found inside a Azure Cloud Shell instance"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://www.michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Underlying Software in Azure Cloud Shell

The Azure Cloud Shell is an extremely powerful feature of Azure and one that I'm a big fan of. In the previous tips, we've talked a bit about [Storage](https://www.michaelcrump.net/azure-tips-and-tricks13/) and then using that [storage to store an SSH key](https://www.michaelcrump.net/azure-tips-and-tricks14/) for a Linux VM. I thought that I should take a step back and talk about the underlying software that is running in an Azure Cloud VM instance. Keep in mind, that I don't work on the Azure Cloud Shell team, this is just my understanding of it. 

When you spin up an Azure Cloud Shell, it create a container that contains things such the OS and other runtimes. By default you get Linux, Node.js and more (covered later). The storage account setup the first time you use Cloud Shell then persist data (like shell scripts, SSH keys, etc.) that you can use once you are connected to the container. It also persist things automatically such as your `.bash_history` and stores your Azure authentication token in `./azure/accessTokens.json`. 

With that information, let's see what is under the hood. Spin up your Azure Cloud Shell now!

### Host Operating System

The container that your Azure Cloud Shell instance is running in is Ubuntu Linux. You can gather additional information about the release with the following commands. 

You can type `lsb_release -a` to see print [OS level distribution information](https://refspecs.linuxfoundation.org/LSB_3.0.0/LSB-PDA/LSB-PDA/lsbrelease.html) that is being used. 

	michael@Azure:~$ lsb_release -a
	No LSB modules are available.
	Distributor ID: Ubuntu
	Description:    Ubuntu 16.04.2 LTS
	Release:        16.04
	Codename:       xenial

You can use `uname -a` to [print information](https://www.computerhope.com/unix/uuname.htm) about the current system.

	michael@Azure:~$ uname -a
	Linux cc-72f9-63c154d-1351310522-4x9jr 4.4.0-93-generic #116-Ubuntu SMP Fri Aug 11 21:17:51 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

Things like `arch` gives you architecture information

	michael@Azure:~$ arch
	x86_64

## You have access to typical Linux apps

You can type `man` for access to the manual. 

	michael@Azure:~$ man
	What manual page do you want?

You can pull up specific pages for help documentation such as `man ls`. 

You have access to vim, nano and other editors. 

<img style="border:3px solid #021a40" src="/files/azuretip15.gif">


### Additional Software Installed in Cloud Shell

The container also contains things like Git, Python, Node.js, .NET Core. You can test this by the following commands: 

	michael@Azure:~$ git --version
	git version 2.7.4
	
	michael@Azure:~$ python --version
	Python 3.5.2
	
	michael@Azure:~$ nodejs -v
	v6.9.4
	
	michael@Azure:~$ dotnet --version
	1.0.1

Neat stuff! I hope this helps with your Azure Cloud journey. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 