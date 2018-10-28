---
layout: post
title: "Azure Tips and Tricks Part 168 - Part 1 - A quick tour around Azure DevOps Projects using Node.js and AKS"
excerpt: "Learn how to use Azure DevOps Projects"
tags: [azure, devops, devops projext, nodejs, kubernetes]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## A quick tour around Azure DevOps Projects and Node.js and Kubernetes Service

* [Part 1 - This post](http://www.michaelcrump.net/azure-tips-and-tricks168/)
* [Part 2 - Coming tomorrow]()
 
In this post, I will walk you through creating a new [Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service/) (AKS) cluster using an [Azure DevOps Projects](https://azure.microsoft.com/en-us/features/devops-projects/) and take a look under the hood to help understand how to get started with AKS.

## Hold up - What is Azure DevOps and AKS (in a nutshell)?

Azure DevOps Services is a cloud service for collaborating on code development such as: 

* Source control
* CD/CD
* Agile tooling
* A variety of tools to test your apps, including manual/exploratory testing, load testing, and continuous testing
* Dashboards
* Built-in wiki

Azure Kubernetes Service (AKS) manages your hosted Kubernetes environment, making it quick and easy to deploy and manage containerized applications without container orchestration expertise. It also eliminates the burden of ongoing operations and maintenance by provisioning, upgrading, and scaling resources on demand, without taking your applications offline.

## Create the DevOps Project

In the Azure portal, search for **DevOps** and choose the **DevOps Project** from the results. Click the **Add** button, select the **Node.js** application, **click** it and then the **Next** button. Select **Express.js** for the application framework and click **Next**. For deploying the application, select **Kubernetes Service** and click Next. Now just give the DevOps project an **Organization name** and **Project name**. Provide a subscription and a **cluster name** and click the **Done** button. 

<img style="border:3px solid #021a40" src="./files/devops-k8s1.gif">

A lot of amazing work is happening in the background, so now is the time to drink a cup of coffee or read my [other tips](http://azuredev.tips) before clicking the **refresh** button on your DevOps Projects list. 

<img style="border:3px solid #021a40" src="./files/devops-k8s2.png">

**Click** on your **DevOps project name** in the list to go to the DevOps project dashboard. This has everything you need to access the source code repository and the application build and release pipeline (which automates the steps needed to take your code, build it and deploy to a live Kubernetes environment).  There are also links to your live deployed application, the Kubernetes cluster and [Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview) (telemetry for your live site).

<img style="border:3px solid #021a40" src="./files/devops-k8s3.png">

You should also have received an email letting you know the project is ready. You can also start setting up your team members. 

<img style="border:3px solid #021a40" src="./files/devops-k8s20.png">

## Taking a peek at the code
In the CI/CD pipeline, **click** on the commit to see the code or you can optionally click on **Master** to take you to the full file list.

<img style="border:3px solid #021a40" src="./files/devops-k8s4.png">

This takes you to the commit for the repo we just deployed containing the deployed sample app.

<img style="border:3px solid #021a40" src="./files/devops-k8s5.png">

When you created the DevOps project, it cloned the source from the [devops-project-samples](https://github.com/Microsoft/devops-project-samples) GitHub project and added it your DevOps projects and did a lot of the initial plumbing for you. How cool is that?

## Taking a look at the Build

Back on the DevOps Project dashboard, click the **Build link** that has the successful build number.

<img style="border:3px solid #021a40" src="./files/devops-k8s6.png">

This takes you to the new Azure DevOps Pipelines build that was created for the project. Now click the **Edit** button at the top.

<img style="border:3px solid #021a40" src="./files/devops-k8s7.png">

You now see the steps created for building a container image and a [Helm package](https://helm.sh/). For those that ned a refresher, **Helm** is used to deploy applications to Kubernetes and it is used by default with the DevOps projects that target Kubernetes.

<img style="border:3px solid #021a40" src="./files/devops-k8s8.png">

Clicking on either of the Docker tasks will show you the new Azure Container Registry (ACR) that the DevOps project created, along with the image name (plus the build number).

<img style="border:3px solid #021a40" src="./files/devops-k8s9.png">

The build creates an ACR, builds and pushes the image using docker, checks to see if Helm is installed begins packaging and deploying the charts/sampleapp directory It also creates the ARM templates and finally publishes the build artifact.

If you switch back over to **Repos**, then **Files** then **Applications** then you can see the `charts/sampleapp` folder. 

<img style="border:3px solid #021a40" src="./files/devops-k8s10.png">

I hope that helps and tomorrow we'll take a look at the **Dev** and **Azure Resources** portion.

**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.