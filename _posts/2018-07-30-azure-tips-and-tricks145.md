---
layout: post
title: "Azure Tips and Tricks Part 145 - Easily reset the Administrator password for an Azure SQL database"
excerpt: "Learn how to easily reset the password for Azure SQL database"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Easily reset the Administrator password for an Azure SQL database

A common scenario that I have heard folks ask is "How do I reset the Admin password for an Azure SQL database that I've forgotten or lost?"

An easy solution to this is 

1. Go to the [Azure portal](https://portal.azure.com)

2. Select **SQL databases**

3. Select the name of the database that you want to change the Admin password.

4. Click on the **Server name url** for the selected database. 

<img style="border:3px solid #021a40" src="/files/azuresqlpw1.png">

5. Reset password is at the top.

<img style="border:3px solid #021a40" src="/files/azureappkudu3.png">

Please note that if you reset the SQL Database server password during a time when there are active connections to databases on the server, you may want to use the KILL statement to terminate user sessions. This will force client connections to refresh their sessions with the database and the host server. 

Thanks for reading!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 