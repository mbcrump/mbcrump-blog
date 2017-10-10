---
layout: post
title: "Azure Tips and Tricks Part 31 - Setting up Email Alerts with Azure App Services"
excerpt: "Learn how to setup email alerts with Azure App Services"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Setting up Email Alerts with Azure App Servicess

**Alerts** allows you to receive an alert based on monitoring metric for your Azure app services. You can be notified in a variety of ways such as the Azure Portal, Webhooks or Email. In this post, we'll setup an alert based on a 404 error message and send it via email. 

In order to take advantage of this, you'll need to log into your Azure account and go to your App Service that you created and look under **Monitoring** then you will see **Alert**. Open it and select **Add Alert** as shown below. 

<img style="border:3px solid #021a40" src="/files/alertblog1.png">

Here you'll see the following options: 

* Resouce - selects which resource you want the alert active on. 
* Name - you'll need to give it a unique name.
* Description (optional) - Provide a description of the alert. Though this is optional, I'd recommend adding one.
* Alert on Metric or Events - You can trigger an alert on some metric or an event. 

**Metric vs. Event**  A metric would be something like "If we receive 5 or more Http Server Errors over the last 5 minutes then trigger an alert". An Event would be if something Started, Stopped, Deleted or all of the above happened with our App Service than trigger an alert. 
{: .notice--info}

Go ahead and select a resource and provide a **Name** and **Description** and select **Http 404** for the metric with the **Greater than** condition set for **O threshold** and **Over the last 5 minutes**. Go ahead and add a checkmark for the email and provide an additional email address as shown below. 

<img style="border:3px solid #021a40" src="/files/alertblog2.png">

Press **OK** and it will save the alert. 

Head back to your website (*.azurewebsites.net) and enter an invalid page to trigger a 404 error. In my case, I entered http://app.azurewebsites.net/**TESTING/**. It should throw an error unless you have a custom error page defined. 

```text
Server Error in '/' Application.

The resource cannot be found.

Description: HTTP 404. The resource you are looking for (or one of its dependencies) could have been removed, had its name changed, or is temporarily unavailable.  Please review the following URL and make sure that it is spelled correctly. 

Requested URL: /TESTING/
```

Take a look at your email and you should see an email from Azure as shown below. 

<img style="border:3px solid #021a40" src="/files/alertblog3.png">

Go back into the Azure Portal and search for **Alerts** and then the alert that you just created. You can see when it was last triggered as well as other information. If you click on the alert, then you'll see you can also do additional things such as run a logic app when this alert triggers. 

<img style="border:3px solid #021a40" src="/files/alertblog4.png">

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--inverse} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 