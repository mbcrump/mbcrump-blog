---
layout: post
title: "Azure Tips and Tricks Part 142 - Quickly edit files within Cloud Shell using Code"
excerpt: "Learn how to quickly edit files within Cloud Shell using Code"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Quickly edit files within Cloud Shell using Code

I recently had a reader that read my **Cloud Shell** list of [Azure Tips and Tricks](https://www.michaelcrump.net/azure-tips-and-tricks-sorted-list/) and noticed that I didn't mention using Code with Cloud Shell. Today's tip is to make that right!

I'm sure by now everyone has used the lovely [Code editor](https://code.visualstudio.com/) in some application before but may not be aware that you use the editor within Cloud Shell without installing anything. To give this a spin, then open up Cloud Shell and type ``code .`` and you'll see the following:

<img style="border:3px solid #021a40" src="/files/azcodeinportal.gif">

Notice that you can do things such as navigate directories, view files with the same syntax used in VS Code and you can easily save, close the editor or open a file outside the current working directory and open the command pallete. 

If you open the command pallete then you'll see a very familiar list of commands that you've probably used in the editor on your desktop. 

<img style="border:3px solid #021a40" src="/files/azcodeinportal1.gif">

And since this is based upon the open-source Monaco project, that powers Visual Studio Code, then you can expect we'll see more features added over time. As of the time of this writing, it automatically includes authorization for pre-installed open source tools like Terraform, Ansible, and InSpec. So what are you waiting for? Go check out [Azure Cloud Shell and Code](http://shell.azure.com) now!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 