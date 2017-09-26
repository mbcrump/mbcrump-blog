---
layout: post
title: "Azure Tips and Tricks Part 23 - Testing Web Apps in Production with Azure App Service"
excerpt: "Learn how to use test Web Apps for production using Azure App Service"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Intro

We've recently created a [web app](http://www.michaelcrump.net/azure-tips-and-tricks19/) and uploaded it to Azure App Service. We also took a look at [multiple ways](http://www.michaelcrump.net/azure-tips-and-tricks20/) to examine those files through the Azure portal interface and how we'd add [extensions](http://www.michaelcrump.net/azure-tips-and-tricks21/) and [deployment slots](http://www.michaelcrump.net/azure-tips-and-tricks22/) for our web app. In this post, we'll look at a feature called `Testing in Production` which isn't as scary as it sounds.  

### Testing Web Apps in Production with Azure App Service

**Hold up!** You'll want to take a look at the [deployment slots](http://www.michaelcrump.net/azure-tips-and-tricks22/) post if you haven't worked with deployment slots before. 
{: .notice--info}

Go to the Azure Portal and select my App Service and click on **Testing in Production** under **Development Tools** to get started. The first thing you'll see is `Static Routing` and you'll notice that it's looking for a deployment slot and traffic percentage. 

**What is Static Routing** This section lets you control how traffic is distributed between your production and other slots. This is useful if you want to try out a new change with a small percentage of requests and then gradually increase the percentage of requests that get the new behavior.
{: .notice--info}

We'll want to split the traffic to our site into 2 groups to test our new site and see if customers like it. Since this is just a demo, I want to send a large number of folks to our new `staging` site as shown below. 

<img style="border:3px solid #021a40" src="/files/testinprodazure7.png">

Great! Now keep in mine that we have two versions of our site. One that is `production` and `staging`. They are identical except for the staging site has a large font that says `jsQuizEngine version 2`. 

We don't want to **swap** sites, we just want to **distribute** traffic between the two site. 

I can test this by going to my production url and refreshing the site until the `staging` site is shown with the production url. 

<img style="border:3px solid #021a40" src="/files/testinprodazure1.gif">

Success! it works, but what happens when they leave the site? We actually store a cookie that keeps track of it. You can find this cookie yourself by expecting the site and looking for the cookie shown below. 

<img style="border:3px solid #021a40" src="/files/testinprodazure2.png">

You could actually force the `old production` site by setting the `x-ms-routing-name` cookie to `self` or providing it in the URL query string such as `http://myquizapplication.azurewebsites.net/?x-ms-routing-name=self`. You could even use the URL to let your users test different versions of your site. For example, I could use `http://myquizapplication.azurewebsites.net/?x-ms-routing-name=staging` to let users try my new web site before I push it live. This is very neat stuff, folks! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 