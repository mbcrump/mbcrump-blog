---
layout: post
title: "Azure Tips and Tricks Part 140 - Easily copy your SQL Azure database to your local development server"
excerpt: "Learn how to easily copy your SQL Azure database to your local development server"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Easily copy your SQL Azure database to your local development server

I've ran across folks at conferences that asked me "How do you copy a SQL Azure database to my local development machine?" While chatting with them, I always found it difficult to understand why (as it is dirt cheap to have a development SQL Azure instance in the cloud) but nevertheless it is their data and there is an easy way to do this. 

First off, [download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017) and connect to your SQL Azure database that you want to copy locally.

**Note by cbattlegear** One important caveat to this process (as shown below). If any writes are happening on the database while you do the export the import will be broken. Best practice is to run `CREATE DATABASE AS COPY` to create a copy of the database and create an export of the copy.
{: .notice--info}

Right-click on the **Database** -> click **Tasks** > **Export data-tier application**

<img style="border:3px solid #021a40" src="/files/sqlazure1.png">

You'll see a wizard and will export your database to a local .bacpac file.

<img style="border:3px solid #021a40" src="/files/sqlazure2.png">

You'll see something similar to this screen once it has finished processing. 

<img style="border:3px solid #021a40" src="/files/sqlazure4.png">

Now ensure you are connected to your local target SQL server instance (or SQL Azure instance) and right-click on the **Database** -> click **Tasks** > **Import data-tier application** and select the .backpac file that you created earlier. 

<img style="border:3px solid #021a40" src="/files/sqlazure3.png">

That is all there is to it. Now you can do anything you wish with that database with no worries about the production database. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 