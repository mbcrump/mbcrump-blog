---
layout: post
title: "Azure Tips and Tricks Part 105 - Day 5 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
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
* [03 Swagger - Learn how to use Swagger for API management](http://www.michaelcrump.net/azure-tips-and-tricks103/)
* [04a Azure Deployment - Deploy the SQL database to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks104/)
* [04b Azure Deployment - Deploy the front-end Web App and API App to Azure manually](http://www.michaelcrump.net/azure-tips-and-tricks105/)
* [05 Adding the project to VSTS with Git](http://www.michaelcrump.net/azure-tips-and-tricks107/) 
* [06 VSTS Continuous Integration - Setup a CI Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks108/) 
* 07 VSTS Continuous Deployment - Setup a CD Process in VSTS (automated deploy to Azure)
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">


We will use Visual Studio to deploy to Azure in this tutorial. This can also be done by packaging up the files and uploading manually to Azure. Or, you could do it via an automated CI/CD (Build and Release) process which will be shown in upcoming posts. 

## Front-end Angular + Back-end API projects

Before we begin, I'm assuming you're using the same email address for VSTS that you are using for Azure. 

1.) Open the solution file in Visual Studio, if it is not already opened. Login to Visual Studio with the same email address that you used to signup for your Azure account. 

2.)  Right click on the API project and choose Publish.

<img style="border:3px solid #021a40" src="/files/e2e-08.png"> 

3.) Choose an App Service.

<img style="border:3px solid #021a40" src="/files/e2e-09.png"> 

4.) Fill in all the settings: add in a name, choose the subscription, create a new resource group. For the App Service Plan: choose a name, the closest location to you and Free. Then on the main modal click **Create**. 

<img style="border:3px solid #021a40" src="/files/e2e-10-1.png"> 

If you are on the **ToDoListAPI** project, make sure you have API selected. 

<img style="border:3px solid #021a40" src="/files/e2e-18.png">

If you are on the **ToDoListAngular** project, make sure you have Web App selected. 

<img style="border:3px solid #021a40" src="/files/e2e-19.png"> 

<img style="border:3px solid #021a40" src="/files/e2e-11.png"> 

5.) Make sure it shows up in the Azure Portal after giving it a few minutes to publish. Click on the API project to go to the overview (red arrow).

<img style="border:3px solid #021a40" src="/files/e2e-12.png"> 

6.) Copy the URL of the API App Service as highlighted in the screen-shot. 

<img style="border:3px solid #021a40" src="/files/e2e-13.png">

7.) Let's connect the front end to the API project.  Open up the **ToDoListAngular** solution.  Go to the **web.config** file of your front end **ToDoListAngular** project. Paste in the URL from the previous step. 

<img style="border:3px solid #021a40" src="/files/e2e-14.png">

8.) Let's do the same publishing to Azure for the front end project.  

**Repeat steps 2-5, BUT do it on the front end ToDoListAngular project. Make sure on Step 4 you choose the right option of "Web App" for the Angular Web project.**

9.) Verify once you are done Publishing that it is in the Azure Portal.  Click on the App Service (red arrow in screenshot). 

<img style="border:3px solid #021a40" src="/files/e2e-15.png">

10.) On the **Overview** page, get the URL and copy it. 

<img style="border:3px solid #021a40" src="/files/e2e-16.png">

11.) Paste the URL into your browser and click on the **Todo** tab to see the Todo list. You should now have a working Azure App Service Web  front end talking to an Azure App Service API which connects to Azure SQL. 

<img style="border:3px solid #021a40" src="/files/e2e-17.png">

Great, so now you've moved your Front-end Angular + Back-end API projects to one hosted in the cloud with Azure! Come back tomorrow and we'll keep moving forward by looking at Git and VSTS integration. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 