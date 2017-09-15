---
layout: post
title: "Azure Tips and Tricks Part 13 - Demystifying storage in Cloud Shell"
excerpt: "Understand what the Azure Cloud Shell is using storage for."
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://michaelcrump.net/azure-tips-and-tricks-complete-list/)

## What's under the hood of Azure Cloud Shell?

The [Azure Cloud Shell](https://azure.microsoft.com/en-us/features/cloud-shell/) is something that I've took for granted since it launched at Build 2017. I always knew that I could use it to run [CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) commands and didn't really stop to think what is "Under the hood"... until now. 

When you first open the Cloud Shell, you will find that it requires you to create a Storage account. The reason for that Storage Account is to persist the scripts, keys, etc that you'll use over and over as you interact with your resources. 

You can find it once you go to your Resource Group and look for `cloud-shell*` as shown below. 

<img style="border:3px solid #021a40" src="https://michaelcrump.net/files/cloudshell1.png">

If you drill down into the Storage account, you'll land on two directories - `.cloudconsole` and `.pscloudshell`. More on that later. 

<img style="border:3px solid #021a40" src="https://michaelcrump.net/files/cloudshell2.png">

Open the Azure Cloud Shell inside of the portal by clicking on the icon at the top (looks like `>_`)

Keep in mind that the Cloud Shell is based off an open-source implementation of [Xterm.js](https://github.com/sourcelair/xterm.js) that emulates the terminal in your browser. It is talking over a web socket to a full Linux BASH shell. Begin by typing:

	michael@Azure:~$ ls -l
	total 0
	lrwxrwxrwx 1 root root 23 Sep 10 16:27 clouddrive -> /usr/michael/clouddrive

Great, we see a clouddrive that is mapped to /usr/michael/clouddrive

Change into that directory and list it out.

	michael@Azure:~$ cd clouddrive
	michael@Azure:~/clouddrive$ ls -l
	total 0
	michael@Azure:~/clouddrive$

Nothing there? Or is there? 

Remember the `.cloudconsole` and `.pscloudshell` directories from above?

	michael@Azure:~/clouddrive$ cd .cloudconsole
	michael@Azure:~/clouddrive/.cloudconsole$ ls
	acc_michael.img

Nice! We just found a `acc_michael.img` file. This is a 5 gig image that persist your home directory. You could have also navigated through the portal to see what was inside this directory but now you under the CLI better! For those that want an extra challenge, go to the Azure Portal and download the Image file and explore it. Feel free to post comments on what you found below. 

So what about the other file called `.pscloudshell`? 

We'll this is for the PowerShell feature coming to the Cloud Shell! You'll have to explore this one for yourself as it is preview at the time of writing. But you can request access now through [this form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR_A6H7yUZotAkPG2p0GxIGFURTUxQzlWWVBKWFpSNlc3RUY1UDg4STFBNS4u)!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 