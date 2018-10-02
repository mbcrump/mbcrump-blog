---
layout: post
title: "Azure Tips and Tricks Part 161 - Change the Azure Function runtime version after Deployment"
excerpt: "Learn how to use change the azure function runtime version after deployment"
tags: [azure, app service, portal, resources]
share: true
comments: true
---
 
**NEW:** The FREE Azure Developer Guide eBook (Fall 2018 Edition) is now [available!](http://aka.ms/azuredevebook)
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}

## Change the Azure Function runtime version after Deployment

If you have used Azure Functions since the beginning, then chances are you've started with a 1.x runtime. Since 2.x is out, you may want to upgrade to it but will be greeted with the following message:

<img style="border:3px solid #021a40" src="/files/changetheazure181001-1.png">

This helps protect users from breaking their Azure Function. As v1 and v2 runtimes are not meant to be interchanged.

If you still want to do this, then you can simply change the `FUNCTIONS_EXTENSION_VERSION` App Setting to `~1` or `~2` to target the runtime that you want.

<img style="border:3px solid #021a40" src="/files/changetheazure181001-2.png">


**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
