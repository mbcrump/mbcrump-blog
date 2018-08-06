---
layout: post
title: "Azure Tips and Tricks Part 146 - Rename an Azure SQL database"
excerpt: "Learn how to easily rename an Azure SQL database"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Rename an Azure SQL database

Last week, I did a SQL post on [Easily reset the Administrator password for an Azure SQL database](http://www.michaelcrump.net/azure-tips-and-tricks145/) and it did rather well. So I'm back with another SQL post that addresses another common scenario that folks ask "How do I rename an Azure SQL database"?

### Rename with command-line - TSQL 

1. Connect with **SQL Server Management Studio** to your Azure database server

2. Right-click on the master database and select **New Query**

3. In the **New Query window** type `ALTER DATABASE [dbname] MODIFY NAME = [newdbname]`. (Make sure you include the square brackets around both database names.)

### Rename with a GUI - SQL Server Management Studio

1. Connect with SQL Server Management Studio 

2. Make sure **Object Explorer** pane is open. 

3. Click on the database name *(as the rename option from the dropdown will be greyed out)* and type in the new name. 

4. The Azure Portal should show the reflected the change almost immediately.

Let me know in the commands if you want me to continue exploring Azure SQL. Thanks for reading!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 