---
layout: post
title: "Azure Tips and Tricks Part 101 - Day 1 - An end to end scenario with Azure App Server, API Apps, SQL, VSTS and CI/CD"
excerpt: "A tutorial on creating a To-Do list app with .NET and using Azure App Server, API Apps, SQL, VSTS and CI/CD"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## A multi-part series showing an end-to-end possibility

[Crystal Tenn](https://www.linkedin.com/in/crystal-tenn-6a0b9b67/) and I teamed up to bring an E2E blog series that features an Azure App Service website that communicates with an API project, which communicates to an Azure SQL back-end. The app is a traditional To-Do application based on an existing sample that used ADO.NET, but adapted for Azure deploy and to Visual Studio 2017. The  technology/tooling stack is Visual Studio, VSTS, C#, Angular, and SQL. 

The process for the app is described below. In Visual Studio, you will start out with a working To Do list application. You will push the code to VSTS (Visual Studio Team Services). Then you will create a CI/CD (Continuous Integration/Continuous Delivery) process in order to deploy to Azure. In Azure you will create 3 resources: Azure Web App, Azure API App, and an Azure SQL Server through this exercise. 

[TOC subject to change]

* [Today - 01 Local Setup - SQL Server](http://www.michaelcrump.net/azure-tips-and-tricks101/) - Locally connect a front-end website to an API, and connect the API to a SQL Server. 
* 02 Swagger - Learn how to use Swagger for API management
* 03 Dapper - Learn how to use Dapper micro-ORM to access to database
* 04a Azure Deployment - Deploy the SQL database to Azure manually
* 04b Azure Deployment - Deploy the front-end Web App and API App to Azure manually
* 05 Adding project to VSTS with Git - I will show you how create a free VSTS account and how to use Git to add your project to VSTS
* 06 VSTS Continuous Integration - Setup a CI Process in VSTS
* 07 VSTS Continuous Deployment - Setup a CD Process in VSTS (automated deploy to Azure)
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img style="border:3px solid #021a40" src="/files/todolist-diagram.png">

## Prerequisites

Please download the required software listed below. If you already have the software and a different version, that is no problem at all, but probably best to use the latest version. If you have access to paid versions of the software, these are fine as well.

The tutorial can be completed for free, but will require a Azure account. Note: The Azure account asks you for a credit card number, but will not charge you at all or "roll into a paid version", it simply expires when your trial month is up.

* [Azure](https://www.azure.com) - Get a free account - You get $200 USD credit a month, these are "free" credits on a trial account and cost you nothing. 
* Visual Studio 2017 - As a note, the instructions will be using Visual Studio 2017. You can get Visual Studio 2017 Community for free here: [https://www.visualstudio.com/vs/community/](https://www.visualstudio.com/vs/community/).
* SQL Server Express: [https://www.microsoft.com/en-us/sql-server/sql-server-editions-express](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express)
* SQL Server Management Studio: [https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)
* Basic understanding of coding & installation 

## Local Setup - SQL Server

The local setup will start with setting up your database.  You will then open the solution in Visual Studio.  You need to connect the API project to your SQL Server.  Then connect your front end Angular project to the API project. 

1.) We'll be working with an existing app. So download [it here](https://github.com/catenn/ToDoList/archive/master.zip) and extract it to a folder on your hard drive.

2.) Open SQL Server Management Studio (SSMS) and click the dropdown on Server Name and choose **Browse for more**.

<img src="/files/e2e-browseformore.jpg">

3.) Choose the Server name of your instance. This name most likely will be in the format **ComputerName\ServerName**.

<img style="border:3px solid #021a40" src="/files/e2e-servers.jpg">

4.) Choose Windows Authentication. Save your **ComputerName\ServerName** in a Notepad, we will need this again later. Hit Connect. 

<img style="border:3px solid #021a40" src="/files/e2e-sqllogin.jpg">

5.) Open the folder that we downloaded earlier by double clicking **ToDoList.sln**. It should open in Visual Studio 2017. 

6.) Right click on the ToDoListDb project and choose **Publish**. 

<img style="border:3px solid #021a40" src="/files/e2e-slnexplorerpublish.jpg">

7.) On the modal, click Edit:

<img style="border:3px solid #021a40" src="/files/e2e-editdbconnection.jpg">

8.) For Server name, take the Notepad value you saved for **ComputerName\ServerName** and enter it here.  Make sure the Database Name is ToDoListDb, but that should be filled in for you. Click OK. 

<img style="border:3px solid #021a40" src="/files/e2e-connection.jpg">

9.) Don't edit any other values on this modal and just hit **Publish**. Note: Test Connection will not work.

<img style="border:3px solid #021a40" src="/files/e2e-publishdb.jpg">

10.) You will see the publish begin.

<img style="border:3px solid #021a40" src="/files/e2e-publish1.jpg">

11.) It is done when you see this:

<img style="border:3px solid #021a40" src="/files/e2e-publish2.jpg">

12.) Go back to **SQL Server Management Studio** and hit refresh:

<img style="border:3px solid #021a40" src="/files/e2e-refresh.jpg">

13.) Your SQL database should look something like this now. 

<img style="border:3px solid #021a40" src="/files/e2e-sqlverify.jpg">

Congrats, we now have our SQL database setup locally. Come back and we'll continue setting up Visual Studio and Swagger. 

Also, follow Crystal and her other amazing work on [GitHub](https://github.com/catenn). We'll both be monitoring comments on this post. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 