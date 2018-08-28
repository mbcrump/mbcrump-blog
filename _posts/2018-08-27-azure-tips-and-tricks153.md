---
layout: post
title: "Azure Tips and Tricks 153 - How to get the Azure Account Tenant Id?"
excerpt: "Learn how to quickly get the Azure Account Tenant ID"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## How to get the Azure Account Tenant Id?

Your Office 365 tenant ID is a globally unique identifier (GUID) that is different than your tenant name or domain. On rare occasion, you might need this identifier, such as when configuring Windows group policy for OneDrive for Business. 

Knowing this, you'll find that there are times when you will want to grab the Tenant Id and while you can do this through PowerShell, sometimes it is just as easy to grab this through the Azure Portal. 

> The **DirectoryId** and **TenantId** both equate to the GUID representing the ActiveDirectory Tenant. Depending on context, either term may be used by Microsoft documentation and products, which can be confusing.

Open the Azure Portal and navigate to **Azure Active Directory**, then **Properties** and copy the **Directory ID**

<img style="border:3px solid #021a40" src="/files/aadazure1.png">

> In other words, the "Tenant ID" IS the "Directory ID".

You can also do this in the Azure CLI:

```text
az account show --subscription a... | jq -r '.tenantId'
az account list | jq -r '.[].tenantId'
```

I hope it helps!

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0m_7PjUWSdOsfLRTa0HuzZUNE1PS1ZNR0pOUktSTUE2Wk0yWUxRQVI1WC4u)
{: .notice--primary}

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 