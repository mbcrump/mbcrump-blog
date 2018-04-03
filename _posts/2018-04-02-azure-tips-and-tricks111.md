---
layout: post
title: "Azure Tips and Tricks Part Part 111 - Deployment Slots for Web Apps using the Azure CLI"
excerpt: "Learn how to work with deployment slots with this quick tutorial"
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

This post was brought to you by [Lohith (kashyapa)](https://www.twitter.com/kashyapa). 
{: .notice--info}

## What are Deployment Slots?

Deployment Slots are a feature of Azure App Service. They actually are live apps with their own hostnames. You can create different slots for your application (for e.g. Dev, Test or Stage). The Production slot is the slot where your live app resides. With deploymet slots, you can validate app changes in staging before swapping it with your production slot. You can read more about deployment slots [here](https://docs.microsoft.com/en-us/azure/app-service/web-sites-staged-publishing "Set up staging environments in Azure App Service").

## Pre-Requisites

* Microsoft Azure Subscription (Sign up for [free](https://azure.microsoft.com/en-us/free/ "Create your Azure free account today"))
* Microsoft Azure CLI (Install from [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest "Install Azure CLI 2.0"))

## Log in to Azure

Before executing any Azure CLI commands, you will need to login first. 

* Open **Command Prompt** or a **Powershell** session
* Enter following command:

`az login`

The command will prompt you to log in with an authentication code via a website.

## Listing Deployment Slots

To list **deployment slots** in an **Azure App Service**, execute the following command:

`az webapp deployment slot list -n "web app name" -g "resource group name"`

## Creating Deployment Slot

To create a **new deployment slot** in an Azure App Service, execute the following command:

`az webapp deployment slot create -n "web app name" -g "resource group name" -s "deployment slot name"`

## Swapping Deployment Slot

To **swap a deployment slot** in an Azure App Service, execute the following command:

`az webapp deployment slot swap -n "web app name" -g "resource group name" -s "source slot name" --target-slot "target slot"`

## Deleting a Deployment Slot

To **delete a deployment slot** in an Azpp Service, execute the following command:

`az webapp deployment slot create -n "web app name" -g "resource group name" -s "deployment slot name"`

## Conclusion

Although Azure portal is a great way to perform most of the Azure related actions, sometimes using the CLI is the easiest. With this tip, we saw how listing/creating/swapping/ deleting deployment slots is just a one line command using the Azure CLI. Hope this helps.

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 