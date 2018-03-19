---
layout: post
title: "Azure Tips and Tricks Part 103 - Day 3 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
excerpt: "A tutorial on creating a To-Do list app with .NET and using Azure App Service, API Apps, SQL, VSTS and CI/CD"
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

* [01 Local Setup - SQL Server](http://www.michaelcrump.net/azure-tips-and-tricks101/) - Locally connect a front-end website to an API, and connect the API to a SQL Server. 
* [02 Local Setup - Visual Studio and Swagger](http://www.michaelcrump.net/azure-tips-and-tricks102/) - Continue Part 1 and use a local instance of Visual Studio and Swagger to communicate to our db.
* [This Post - 03 Swagger - Learn how to use Swagger for API management](http://www.michaelcrump.net/azure-tips-and-tricks103/)
* [04a Azure Deployment - Deploy the SQL database to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks104/)
* [04b Azure Deployment - Deploy the front-end Web App and API App to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks105/)
* 05 Adding project to VSTS with Git - I will show you how create a free VSTS account and how to use Git to add your project to VSTS
* 06 VSTS Continuous Integration - Setup a CI Process in VSTS
* 07 VSTS Continuous Deployment - Setup a CD Process in VSTS (automated deploy to Azure)
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">

## Local Setup - Working with Swagger

If you noticed in the last post, we started working with Swagger. 

**What is Swagger UI?** is a collection of HTML, Javascript, and CSS assets that dynamically generate beautiful documentation from a Swagger-compliant API. 
{: .notice--info}

The nice thing about Swagger is that you can create an existing **Web API** app using the VS Templates and add **Swagger** via Nuget. 

<img style="border:3px solid #021a40" src="/files/e2e-swagger1.jpg">

Then if you spin up a project, you simply add **/swagger** to see the UI. In the example below, we've already added it and supplied the comments in the app to where it recognizes it. This makes testing APIs very simply and it works in real-time, meaning if you run a **POST**, then you can immediately check your database for the new record. 

Learn more about Swagger [here](https://github.com/swagger-api/swagger-ui).

## Continuing where we left off

1.) Open the project in Visual Studio by double clicking **ToDoList.sln**, if it is not already open from the previous parts. Navigate to the **ToDoListDataAPI** project. 

2.) Set the ToDoListDataAPI project to Set as Startup project by right clicking on the project and choosing that option and run the application.

<img style="border:3px solid #021a40" src="/files/e2e-setstartup.jpg">

3.) Add "/swagger" to the end of your URL if it is not already there, you should see a page like this: 

<img style="border:3px solid #021a40" src="/files/e2e-swagger.jpg">

Click on the **Show/Hide** button.

4.) Run a **GET** which is the first API on the page /api/ToDoList, you should see:

<img style="border:3px solid #021a40" src="/files/e2e-02.png">

5.) Run a **POST**, click where the screen-shot shows, and fill in an ID with a random number and any description you want and then click **Try it out**.

<img style="border:3px solid #021a40" src="/files/e2e-03.png">

6.) Run a **GET** again, you should see your added value:

<img style="border:3px solid #021a40" src="/files/e2e-04.png">

7.) Run a **PUT**, again click to get the format from where it's shown in the screen-shot and modify an existing record's description.

<img style="border:3px solid #021a40" src="/files/e2e-05.png">

8.) Try to run a **GET** by ID, use 1 for example:

<img style="border:3px solid #021a40" src="/files/e2e-06.png">

9.) Switch back to SQL Server Management Studio (and log in if you need to) and choose **Select Top 1000 Rows** on the **ToDoListDb** db to see the data.

<img style="border:3px solid #021a40" src="/files/e2e-sqlselect.jpg">

10.) Your SQL Server Management Studio table should look like this now:

<img style="border:3px solid #021a40" src="/files/e2e-sqlserver.jpg">

Come back next week and we'll take a look at [Dapper](https://github.com/StackExchange/Dapper) which is a object mapper for .NET that we used to make our code easy to read and work with the database as well as getting the database into Azure.


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 