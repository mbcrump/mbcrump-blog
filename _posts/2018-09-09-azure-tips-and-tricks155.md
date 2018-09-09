---
layout: post
title: "Azure Tips and Tricks 155 - Archive the Azure Activity Log"
excerpt: "Learn how to archive the Azure Activity Log"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Archive the Azure Activity Log

The Azure Activity Log is a subscription log that provides insight into subscription-level events that have occurred in Azure. This includes a range of data, from Azure Resource Manager operational data to updates on Service Health events.  You may want to Archive the Azure Activity Log if you want to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup. In this post, I'll show you now to archive it with a couple of clicks. 

In the portal, search for the **Activity Log** service. Now click on the **Export** button as shown below:

<img style="border:3px solid #021a40" src="/files/azactivitylog1.png">

Select a Subscription, Region and place a checkmark in the **Export to an Azure Storage Account**. Now use the slider to select a number of days (0 to 365) for which Activity Log events should be kept in your storage account. You can may also select 0 to save it indefinitely. Now click Save.

<img style="border:3px solid #021a40" src="/files/azactivitylog2.png">

Now your logs are safe and sound for the time you specified. 

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 