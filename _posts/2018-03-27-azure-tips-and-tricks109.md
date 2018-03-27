---
layout: post
title: "Azure Tips and Tricks Part 109 - Day 8 - An end to end scenario with Azure App Service, API Apps, SQL, VSTS and CI/CD"
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
* [06 VSTS Continuous Integration - Setup a CI Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks108/) 
* [07 VSTS Continuous Deployment - Setup a CD Process in VSTS](http://www.michaelcrump.net/azure-tips-and-tricks109/) 
* 08 Cleanup - Cleanup and delete the Azure resources created in this tutorial.

Keep in mind : While we won't be going into the deep specifics of how to code, you should be able to use this guide to look at several parts of the Azure technology stack and how you can best implement them in your organization. 

<img src="/files/todolist-diagram.png">

# VSTS Continuous Deployment

1.) On the top menu of **VSTS**, click on **Build and Release**, then choose **Releases** from the drop-down:

<img style="border:3px solid #021a40" src="/files/blog7-mc9.jpg">

2.) On the left, click the **"+" button** and choose **Create release definition**. 

<img style="border:3px solid #021a40" src="/files/blog7-mc10.jpg">

3.) Choose the **Azure App Service Deployment template** and hit **Apply**.

<img style="border:3px solid #021a40" src="/files/blog7-mc11a.jpg">

4.) On the right side, name the environment **Production**, then click the **X** on the top left to close this. 

<img style="border:3px solid #021a40" src="/files/blog7-mc12a.jpg">
 
5.) On the left, click **Add artifact**. 

<img style="border:3px solid #021a40" src="/files/blog7-mc12b.jpg">

6.) For the **artifact**, choose **Build**, and choose the **FE-Angular-CI** (or whatever it is named) build, hit **Add**.

<img style="border:3px solid #021a40" src="/files/blog7-mc12c.jpg">

7.) Click **Tasks**.

<img style="border:3px solid #021a40" src="/files/blog7-mc13.jpg">

8.) Rename your **Release definition** by clicking by the **name**:

<img style="border:3px solid #021a40" src="/files/blog7-mc14.jpg">

9.) Choose your **Azure Subscription**. Choose the **Web App** type.  Choose the **App Service name** you used for the Angular web app. 

<img style="border:3px solid #021a40" src="/files/blog7-mc15.jpg">

10.) Scroll down more on the same page, click the 3 dots under **Package or folder**.

<img style="border:3px solid #021a40" src="/files/blog7-mc16.jpg">

11.) On the modal, choose **ToDoListAngular.zip**, then hit **OK**. 

<img style="border:3px solid #021a40" src="/files/blog7-mc17.jpg">

12.) Click the **"+"** button to add an **additional task.** Choose the **Azure App Service Deploy task**. 

<img style="border:3px solid #021a40" src="/files/blog7-mc17a.jpg">

13.) Select the **new task** on the left. Then, on the right add your **Azure subscription** again. Choose **API App**. Select the **API App Service** that you created in the Azure Portal. 

<img style="border:3px solid #021a40" src="/files/blog7-mc18a.jpg">

14.) Scroll down on the same task, click the 3 dots under **Package or folder**.

<img style="border:3px solid #021a40" src="/files/blog7-mc18b.jpg">

15.)  On the modal, choose **ToDoListDataAPI.zip**, then hit **OK**. 

<img style="border:3px solid #021a40" src="/files/blog7-mc18c.jpg">

16.) Click **Save** at the top. 

<img style="border:3px solid #021a40" src="/files/blog7-mc19.jpg">

17.) Click **Release**, then **Create Release**.

<img style="border:3px solid #021a40" src="/files/blog7-mc20.jpg">

18.) A notification with the name of the release will show up, click on this:

<img style="border:3px solid #021a40" src="/files/blog7-mc21.jpg">

19.) Click **Logs**, then it will bring you to the logs which will display live results. 

<img style="border:3px solid #021a40" src="/files/blog7-mc22.jpg">

20.) Wait until it finishes and shows **Success**.

<img style="border:3px solid #021a40" src="/files/blog7-mc23.jpg">

21.) Go to your **Azure Portal**. Choose your resource from **All Resources**, click on the **name** of the resource.  

<img style="border:3px solid #021a40" src="/files/blog7-mc24.jpg">

22.) View the **overview page** to get the URL:

<img style="border:3px solid #021a40" src="/files/blog7-mc25.jpg">

23.) Your completed page should look like this (hit the link with the red arrow to go to the To Do list!): 

<img style="border:3px solid #021a40" src="/files/blog7-mc26.jpg">

Come back next week and we'll learn how to delete the resources from this tutorial.

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 