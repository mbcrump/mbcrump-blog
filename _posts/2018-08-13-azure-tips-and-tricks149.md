---
layout: post
title: "Azure Tips and Tricks Part 149 - Use PowerShell to quickly see if your Deployment Slot Swapped Successfully"
excerpt: "Learn how to run share business logic between Azure Functions"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Use PowerShell to quickly see if your Deployment Slot Swapped Successfully

A common scenario after sending a swap action to Azure App Service is to check its progress. While you can easily use the Azure Portal, another alternative that I often use is PowerShell. 

You'll quickly learn that `Microsoft.Web/sites/slots/slotsswap/action` contains the information "Succeeded" that you are looking for at the 50th character if you start digging around in the PowerShell and Azure docs.

We can wrap this up in a bow with the following line:

```powershell
$a = Get-AzureRmLog -ResourceGroupName <ResourceGroupName> | Where-Object { $_.operationname.value -contains "Microsoft.Web/sites/slots/slotsswap/action" -and $_.Status.Value -eq 'Succeeded'} 
$a | select { $_.eventtimestamp,$_.operationname.value,$_.status.value,$_.resourceid.substring(50) }
```

Now if you paste this in PowerShell, you should get the following:

<img style="border:3px solid #021a40" src="/files/powershellslot1.png">

As always, I hoped this help someone out there! 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 