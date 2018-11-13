---
layout: post
title: "Azure Tips and Tricks Part 173 - Get the most out of Azure Advisor"
excerpt: "Learn how to use Azure Advisor"
tags: [azure, azure advisor, high availability, security, performance, cost]
share: true
comments: true
---
 
**ATTENTION:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now! No registration required. 
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## Get the most out of Azure Advisor
 
[Azure Advisor](https://azure.microsoft.com/services/advisor/) is a simple dashboard that helps you implement best practices across your Azure resources. In this blog post, I’ll walk you through the types of recommendations it provides and how easy it is to implement them.
 
### Recommendation categories

Advisor looks at the Azure resources in your subscriptions and comes up with recommendations that fall into these categories:
* [High Availability](https://docs.microsoft.com/azure/advisor/advisor-high-availability-recommendations): Suggestions that are important for business-critical and production-worthy applications.
* [Security](https://docs.microsoft.com/azure/advisor/advisor-security-recommendations): Advice to help you prevent and detect threats or security vulnerabilities.
* [Performance](https://docs.microsoft.com/azure/advisor/advisor-performance-recommendations): Recommendations that are tailored to the configurations of your resources and that compile together items from [SQL Database Advisor](https://docs.microsoft.com/azure/sql-database/sql-database-advisor), [Redis Cache Advisor](https://docs.microsoft.com/azure/redis-cache/cache-configure#redis-cache-advisor), and other best practices.
* [Cost](https://docs.microsoft.com/azure/advisor/advisor-cost-recommendations): Information on past usage of things like VMs generates cost-saving recommendations as well as sizing and other resource configurations that affect cost.

### Use Advisor to implement recommendations

Inside the Azure portal, search for **Advisor** and open the **Advisor recommendations** dashboard. At first glance, we can see Advisor has a few recommendations for me, one performance, two for high availability and three for security. At the bottom of the screen, you'll also notice that you can export the recommendations to PDF or CSV files - which is great for mangers to prove you need to work on this task. It is very cool that Azure is watching my back "out of the box"!

<img style="border:3px solid #021a40" src="/files/advisor1.png">

If you’re following along in your own Azure subscription, chances are good you have some recommendations available on the **Advisor dashboard**. 

Let’s take a look at the High Availability recommendations I have.

**Click** on the **High Availability** box in the dashboard.

<img style="border:3px solid #021a40" src="/files/advisor2.png">

You now see more information about the recommendations, like the impact (high, medium, low), description, potential benefits, impacted resources, and the last time the recommendation was updated.

**Click** on an **item** in the recommendation list to learn the complete details.

<img style="border:3px solid #021a40" src="/files/advisor3.png">

The recommendation I selected was the **“Enable Soft Delete to protect blob data.”** In my case, I do think it’s a good idea to turn that on for one of the two storage account it lists. So, I clicked on the **“Enable Soft Delete to protect blob data”** link to get to where I can turn that feature on. Isn’t that cool? Not only did it tell me it was a good idea, but it walks me through what I need to do to follow the recommendation!

<img style="border:3px solid #021a40" src="/files/advisor4.png">

Once I click **Enabled**, I set the Retention policies to **30 days** and click **Save**, that’s it! Now I can use the breadcrumbs in the top to go back to the Enable Soft Delete list. 

Next, I want to select **Postpone** for the other storage account.

<img style="border:3px solid #021a40" src="/files/advisor5.png">

Since I know I don’t want soft delete enabled on this account, I can postpone this recommendation to **Never** and click the **Postpone** button so it doesn’t make the recommendation next time I take a look at Advisor.

If you click on the **Security** tab and drill into a recommendation, then you'll see an actual secure score. This allows you to quickly see which security recommendations pose the greatest threat.

<img style="border:3px solid #021a40" src="/files/advisor6.png">

Again, we see that not only did it tell me what posed the greatest threat, but it walks me through what I need to do to follow the recommendation.

## Summary

To sum it up, the flow for all four categories of recommendations is:
1. Select the recommendation category in the dashboard.
2. Select the individual recommendation.
3. If you want to ignore, you can postpone (or, for security recommendations, use “dismiss”).
4. If you want to implement, select the recommendation item and Advisor will walk you through the steps you need to implement the recommendation.

Implementing best practices is that easy!

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.