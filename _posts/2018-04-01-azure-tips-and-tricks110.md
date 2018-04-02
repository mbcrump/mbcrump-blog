---
layout: post
title: "Azure Tips and Tricks Part Part 110 - Day 9 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
excerpt: "A tutorial on creating a To-Do list app with .NET and using Azure App Service, API Apps, SQL, VSTS and CI/CD"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Tips and Tricks Videos are NOW Available!** : Get all the goodness of Azure Tips and Tricks in video form. [Read more about it here](http://www.michaelcrump.net/azure-tips-and-tricks106/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## A multi-part series showing an end-to-end possibility

[Crystal Tenn](https://www.linkedin.com/in/crystal-tenn-6a0b9b67/) and I teamed up to bring an E2E blog series that features an Azure App Service website that communicates with an API project, which communicates to an Azure SQL back-end. The app is a traditional To-Do application based on an existing sample that used ADO.NET, but adapted for Azure deploy and to Visual Studio 2017. The technology/tooling stack is Visual Studio, VSTS, C#, Angular, and SQL. 

The process for the app is described below. In Visual Studio, you will start out with a working To Do list application. You will push the code to VSTS (Visual Studio Team Services). Then you will create a CI/CD (Continuous Integration/Continuous Delivery) process in order to deploy to Azure. In Azure you will create 3 resources: Azure Web App, Azure API App, and an Azure SQL Server through this exercise. 

* [Local Setup - SQL Server](http://www.michaelcrump.net/azure-tips-and-tricks101/) - Locally connect a front-end website to an API, and connect the API to a SQL Server. 
* [Local Setup - Visual Studio and Swagger](http://www.michaelcrump.net/azure-tips-and-tricks102/) - Continue Part 1 and use a local instance of Visual Studio and Swagger to communicate to our db.
* [Swagger - Learn how to use Swagger for API management](http://www.michaelcrump.net/azure-tips-and-tricks103/)
* [Azure Deployment - Deploy the SQL database to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks104/)
* [Azure Deployment - Deploy the front-end Web App and API App to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks105/)
* [Adding the project to VSTS with Git](http://www.michaelcrump.net/azure-tips-and-tricks107/) 
* [VSTS Continuous Integration - Setup a CI Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks108/) 
* [VSTS Continuous Deployment - Setup a CD Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks109/) 
* [Cleanup - Cleanup and delete the Azure resources created in this tutorial](http://www.michaelcrump.net/azure-tips-and-tricks110/)

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">


## Clean-up Resources 

We've finally made it to the end of the series and I wanted to use this post to remind you to delete the resources that you created in Azure during this tutorial or during development. 

If you want to remove your resources from Azure now, please see the below instructions:

1.)  Go to the **Azure Portal**. Click on the **resource group name** (whatever you named it).

2.) Click **All Resources**.

<img style="border:3px solid #021a40" src="/files/blog10-mc01.jpg">

3.) Click **Delete** Resource Group.

<img style="border:3px solid #021a40" src="/files/blog10-mc02.jpg">

4.) Confirm the **name**, and click **Delete**. 

<img style="border:3px solid #021a40" src="/files/blog10-mc03.jpg">

That's a wrap for this 9 day series! But don't worry, there is plenty more Azure Tips and Tricks coming!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 