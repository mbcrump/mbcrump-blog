---
layout: post
title: "Azure Tips and Tricks Part 156 - Use Azure Logic Apps to Detect when a new SQL record is inserted"
excerpt: "Learn how to use Azure Logic Apps to detect when a new SQL record is inserted"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use Azure Logic Apps to Detect when a new SQL record is inserted

I recently needed the ability to detect when a new SQL record was added and send an email. Since the customer didn't want the existing logic in their app to be modified, I relied on Azure Logic Apps and all their powerful connectors. 

In the portal, create a new **Azure Logic App** and then select **Start with a blank template**. Under the trigger, choose **New step > Add an action**.

In the search box, enter "sql" as your filter. and pick **When an item is created**. 

<img style="border:3px solid #021a40" src="/files/logicsql1.png">

You'll be prompted for connection details, so do so now.

<img style="border:3px solid #021a40" src="/files/logicsql2.png">

Now you'll need to select the **Table Name** and how often you want to check for item. We are going to go with every 5 seconds. 

<img style="border:3px solid #021a40" src="/files/logicsql3.png">

Now choose, **New step > Choose an action**.

In the search box, enter "email" as your filter. and pick **Send an email**. 

<img style="border:3px solid #021a40" src="/files/logicsql4.png">

Type the email address and select which fields to send. You can put custom text as shown below:

<img style="border:3px solid #021a40" src="/files/logicsql5.png">

Now insert a record into your database and it should fire (as long as you have the Logic app running)

<img style="border:3px solid #021a40" src="/files/logicsql6.png">

Easy enough!

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 