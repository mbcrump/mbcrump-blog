---
layout: post
title: "Azure Tips and Tricks Part 104 - Day 4 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
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


# Deploy SQL Database to Azure SQL

1.) Log into the Azure Portal at [portal.azure.com](https://portal.azure.com) if you aren't already logged in.

2.) Create a new SQL Database. Click **New**, select **Databases**, choose **SQL Database**, then lastly hit **Create**.

<img style="border:3px solid #021a40" src="/files/e2e-01SelectSQLDBPortal.png">

3.) Click on **Server and Pricing Tier** to get a slideout options. In the **Server slideout**, make sure you create a username and password and keep it somewhere safe as you will need this to login using SQL Server Management Studio (SSMS).  In the **Pricing Tier**, change to **Basic** so it only costs about $5 per month. Your screen will look approximately like this:

<img style="border:3px solid #021a40" src="/files/e2e-02DBOptions.png">

4.) Click on **All Resources** on the left menu. You should see your new SQL Server and SQL Database. Click on the **SQL Database**. 

<img style="border:3px solid #021a40" src="/files/e2e-03AllResources.png">

5.) On the **Overview** tab. Copy the Server name to seomewhere safe. Click on the **Show Connection Strings**  and copy it somewhere safe.

<img style="border:3px solid #021a40" src="/files/e2e-05DatabaseOverview.png">

The **connection string** will look like this (save this in a Notepad for the web.config in the solution later):

<img style="border:3px solid #021a40" src="/files/e2e-06ConnectionString.png">

6.) Open **SSMS** and enter the **Server name, username, and password** as shown below. 

<img style="border:3px solid #021a40" src="/files/e2e-07SSMS.png">
      
**Note** if you cannot login, please go to the Portal and add your **IP address** by clicking on the **SQL Server** you created, then going to **Firewall**.
{: .notice--info}

<img style="border:3px solid #021a40" src="/files/e2e-10.PNG">

7.) Go back to [Day 1](https://www.michaelcrump.net/azure-tips-and-tricks101/) and repeat steps 6-13, except use the **Azure SQL Server name** that we created earlier instead of your local DB. 

8.) Once the DB has been saved to Azure, go into the **connection strings** of your API project that can be found in the **web.config** as shown below.

<img style="border:3px solid #021a40" src="/files/e2e-webconfig.jpg">

9.) In the **web.config**, change your **connection string** so that it points to your **Azure SQL Server connection string** (that you should have saved into Notepad earlier). Make sure you add your username and password for your Azure SQL Server into the connection string. 

<img style="border:3px solid #021a40" src="/files/e2e-webconfig3.jpg">

Great, so now you've moved your local instance of SQL db to one hosted in the cloud with Azure! Come back tomorrow and we'll keep moving forward by moving using Azure Deployment to move our Web App & API App to the cloud. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 