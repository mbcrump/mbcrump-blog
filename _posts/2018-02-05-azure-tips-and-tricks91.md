---
layout: post
title: "Azure Tips and Tricks Part 91 - Part 2 - Implementing Azure Search with SQL Server"
excerpt: "Learn how to implement Azure Search with SQL Server"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Implementing Azure Search with SQL Server and ASP.NET MVC

In this series I'll cover Azure Search, SQL Server and putting it all together in a ASP.NET MVC web app. The complete list can be found below:

* [Part 1](http://www.michaelcrump.net/azure-tips-and-tricks90/)
* [This post - Part 2](http://www.michaelcrump.net/azure-tips-and-tricks91/)


## Implementing Azure Search

Yesterday, we learned that Azure Search is a search-as-a-service that allows you to search over your content using web, desktop or mobile apps. There is variety of services that you can attach Azure Search to, including SQL Server - which we covered yesterday. Today we'll walk through adding Azure Search to our existing SQL Server instance. 

Open the Azure Portal, and navigate to your SQL Server instance and begin by looking at the  **Settings** pane:

<img style="border:3px solid #021a40" src="/files/azuresearchsql1.png">

Select a **Add Azure Search** and fill out the fields specified below and make sure to select the price as free. 

<img style="border:3px solid #021a40" src="/files/azuresearchsql2.png">

Under **Data Source**, we can easily connect to our Azure SQL Database, we'll need to give it a name, provide the userid and password (that we specified when setting up the SQL db) and press **Test Connection**. If everything goes well, then you'll be able to select the **Customer** table.

<img style="border:3px solid #021a40" src="/files/azuresearchsql3.png">

We'll need to set an index. So give it a name and select **CustomerID** as our Key. We'll now clean up our fields, by deleting ones that we don't want and making sure the fields can be retrieved, sorted, filtered and are searchable by adding a check. 

<img style="border:3px solid #021a40" src="/files/azuresearchsql4.png">

We need to create an indexer to run. I'm going to select the **Daily** schedule and set my watermark column to the **ModifiedDate** as I assume data is unique in that column. 

<img style="border:3px solid #021a40" src="/files/azuresearchsql5.png">

Once you kick that off, you'll see the following notification. It states you can check the monitor progress and once complete you can start searching. 

<img style="border:3px solid #021a40" src="/files/azuresearchsql6.png">

If you go ahead and click on the link on the notification window, then you'll see the following screen.

<img style="border:3px solid #021a40" src="/files/azuresearchsql7.png">

Go ahead and press the Run button and it will start immediately and eventually you'll see it has completed. 

<img style="border:3px solid #021a40" src="/files/azuresearchsql8.png">

Excellent! Our SQL database and Azure Search indexer is in place. Come back tomorrow and we'll kick the tires with a couple of queries against our new index. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 