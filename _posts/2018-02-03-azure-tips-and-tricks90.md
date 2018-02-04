---
layout: post
title: "Azure Tips and Tricks Part 90 - Part 1 - Implementing Azure Search with SQL Server and ASP.NET MVC"
excerpt: "Learn how to implement search using SQL Server and ASP.NET MVC"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Implementing Azure Search with SQL Server and ASP.NET MVC

Welcome to a new series, in this series I'll cover Azure Search, SQL Server and putting it all together in a ASP.NET MVC web app. I'll be adding the post to this series below as I go:

* [Part 1 - Implementing Azure Search with SQL Server and ASP.NET MVC](http://www.michaelcrump.net/azure-tips-and-tricks90/)


## What is it? 

Azure Search is a search-as-a-service cloud solution that allows you to access APIs (REST and an SDK) to search over your content using web, desktop or mobile apps. There is variety of services that you can attach Azure Search to, including SQL Server - which we'll cover in this tutorial. 

## First Step - Creating the SQL Server Database that we'll place the indexer

Go into the Azure Portal and search for SQL Server and click the Add button. 

Give it a database name, resource group and fill out the new server information. For the source, select **AdventureWorksLT** and pricing tier select **Basic**. 

Your screen should look like the following: 

<img style="border:3px solid #021a40" src="/files/azuresearch1.jpg">

**Remember this!** Double check you selected the select **AdventureWorksLT** database if you want to follow along with this tutorial. 
{: .notice--primary}

## Take a look at the data

Now that we have a sample database and it has deployed, let's use **Query Editor** which is inside the SQL Server blade to take a look at the table structure. Note: You can also use [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) if you prefer it better. 

If you click on **Query Editor** and login as instructed, then you'll see the following:

<img style="border:3px solid #021a40" src="/files/azuresearch2.png">

As you can see, I expanded the **Table** dropdown and I can drill down again to the column names. 

It looks like **Customer** would be a great table to implement search and we could pass in the FirstName or LastName field. 

<img style="border:3px solid #021a40" src="/files/azuresearch3.png">

We could write a simple query such as `select FirstName, LastName from SalesLT.Customer ` and click Run to take a look at the data. 

<img style="border:3px solid #021a40" src="/files/azuresearch4.png">

Now that we have our database in place and some solid data to work with, we'll implement Azure Search tomorrow. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 