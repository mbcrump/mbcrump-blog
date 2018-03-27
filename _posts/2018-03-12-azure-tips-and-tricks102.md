---
layout: post
title: "Azure Tips and Tricks Part 102 - Day 2 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
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
* [07 VSTS Continuous Deployment - Setup a CD Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks109/) 
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">

## Local Setup - Visual Studio to talk to our SQL Database

1.) Open the project in Visual Studio by double clicking **ToDoList.sln**, if it is not already open from Part 1.

2.) Open the **Web.config** file of the **ToDoListDataAPI** project. Make sure you are in the right project. 

<img style="border:3px solid #021a40" src="/files/e2e-webconfig.jpg">

3.) Edit the "**ComputerName\ServerName**" highlighted and change it to your computer & SQL server name that you saved in a Notepad. 

<img style="border:3px solid #021a40" src="/files/e2e-webconfig2.jpg">

Mine looks like: 

```text
    <add name="todoItems" connectionString="Server=MICHAELCRUM0FD9\SQLEXPRESS;Initial Catalog=todolistdb;MultipleActiveResultSets=False;Integrated Security=True" providerName="System.Data.EntityClient" />
```

4.) Save the file and set the ToDoListDataAPI project to Set as Startup project by right clicking on the project and choosing that option.

<img style="border:3px solid #021a40" src="/files/e2e-setstartup.jpg">

5.) Hit F5 or Run inside of any browser. 

<img style="border:3px solid #021a40" src="/files/e2e-run.jpg">

Note: If you get **The Web server is configured to not list the contents of this directory.**, then just proceed to step 6. 
{: .notice--info}

6.) Add /swagger to the URL if it is not already there for you. The page should look like this if everything is working properly:

<img style="border:3px solid #021a40" src="/files/e2e-swagger.jpg">

7.) Click Show/Hide to get a full list of APIs available to the application.

<img style="border:3px solid #021a40" src="/files/e2e-showhide.jpg">

8.) Click on **Get** (the first one in the list) to expand it. Click **Try it out!**. If you get a 200 Response Code, it worked! Also take note of the URL port number in your browser. 

<img style="border:3px solid #021a40" src="/files/e2e-get.jpg">

<img style="border:3px solid #021a40" src="/files/e2e-get1.jpg">

9.) Switch back over to Visual Studio and go to the **Web.config** in the **ToDoListAngular** project.  

<img style="border:3px solid #021a40" src="/files/e2e-angularprojwebconfig.jpg">

10.) Make sure that the port number matches the port from the last step.

<img style="border:3px solid #021a40" src="/files/e2e-angularwebconfig.jpg">

11.)  Set the **ToDoListAngular** project as Startup Project. 

<img style="border:3px solid #021a40" src="/files/e2e-angularstart.jpg">

12.)  Hit F5 or hit Run 

13.) You should see the Angular app running in your web browser:

<img style="border:3px solid #021a40" src="/files/e2e-todohome.jpg">

14. Click on Todo list menu and add an entry. Try editing it and deleting it. You can put breakpoints in the code to learn more about how it is performing the CRUD operations. You can also check the SQL database to see the entries. 

<img style="border:3px solid #021a40" src="/files/e2e-todolist.gif">

<img style="border:3px solid #021a40" src="/files/e2e-sql1.jpg">

Congrats, we now have our SQL database and web front/backend setup locally. Come back and we'll look deeper into Swagger. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 