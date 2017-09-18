---
layout: post
title: "Azure Tips and Tricks Part 7 - Use the Table Parameter in the Azure CLI"
excerpt: "Learn how to use the table parameter in the Azure CLI"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://www.michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Use the Table Parameter in the Azure CLI

By default the Azure CLI 2.0 returns results from a command in JSON. You can easily modify this by adding `--output Table`. Try out the command found in the Gif below with `az vm image list-publishers --location NorthCentralUS --output Table`

<img style="border:3px solid #021a40" src="/files/azuretip7.gif">


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 