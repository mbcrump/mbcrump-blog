---
layout: post
title: "Azure Tips and Tricks Part 107 - Day 6 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
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

[TOC subject to change]

* [01 Local Setup - SQL Server](http://www.michaelcrump.net/azure-tips-and-tricks101/) - Locally connect a front-end website to an API, and connect the API to a SQL Server. 
* [02 Local Setup - Visual Studio and Swagger](http://www.michaelcrump.net/azure-tips-and-tricks102/) - Continue Part 1 and use a local instance of Visual Studio and Swagger to communicate to our db.
* [03 Swagger - Learn how to use Swagger for API management](http://www.michaelcrump.net/azure-tips-and-tricks103/)
* [04a Azure Deployment - Deploy the SQL database to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks104/)
* [04b Azure Deployment - Deploy the front-end Web App and API App to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks105/)
* [05 Adding the project to VSTS with Git](http://www.michaelcrump.net/azure-tips-and-tricks107/) 
* 06 VSTS Continuous Integration - Setup a CI Process in VSTS
* 07 VSTS Continuous Deployment - Setup a CD Process in VSTS (automated deploy to Azure)
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">

**Pre-requisite:** Install [Git](https://git-scm.com/downloads)

## Create the VSTS Account

1.) Sign up for VSTS if you do not have an account by clicking the [Sign Up button](https://www.visualstudio.com/team-services/) on the homepage. 

Make sure to use the same email address that you used for Azure.
{: .notice--info}

2.) Create a new VSTS Account by hitting the button on the top right. 

<img style="border:3px solid #021a40" src="/files/blog5-00.png">

3.) After your account is created, then you'll see the following:

<img style="border:3px solid #021a40" src="/files/blog5-mc1.png">

4.) You can optionally rename the project by clicking on the **Gear** icon and clicking on the **Project Name**. Note that if you do this, it updates all of your version control paths, work items, queries, and other team project artifacts to reflect the new name. 

<img style="border:3px solid #021a40" src="/files/blog5-mc2.png">

5.) Click on the **push an existing repository from the command line** and copy the copy to notepad. 

<img style="border:3px solid #021a40" src="/files/blog5-mc3.png">

6.) If you've already installed [Git](https://git-scm.com/downloads), then run navigate to your Visual Studio solution and run the following commands in order. You'll need to change the 4th command to the URL you copied earlier

```text 
git init
git add .
git commit -m "Initial commit"
git remote add origin https://YOURPROJECT.visualstudio.com/_git/AzureWebApp
git push -u origin --all
```

<img style="border:3px solid #021a40" src="/files/blog5-mc04.png">

7.) Go to VSTS and click **Code**, you should see your code there:

<img style="border:3px solid #021a40" src="/files/blog5-05.png">


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 