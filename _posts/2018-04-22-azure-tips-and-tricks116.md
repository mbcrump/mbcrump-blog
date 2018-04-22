---
layout: post
title: "Azure Tips and Tricks Part 116 - Easily Upload and download Azure dashboards"
excerpt: "A tutorial on how to easily Upload and download Azure dashboards"
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

## Easily Upload and download Azure dashboards

Azure has recently added the ability for you to download or upload an existing Azure dashboard with just a couple of clicks. Previously, you had to use a separate tool like **Azure Resource Explorer** to get this data. Now, you'll see a new **Download** and **Upload** option on your Azure Dashboard as shown below:

<img style="border:3px solid #021a40" src="/files/azportal1.png">



Once you download the file it will be in a JSON format. Below is a short snippet that list my **Linux VM** that is on my portal page. 

```json
"1": {
"position": {
	"x": 4,
	"y": 0,
	"colSpan": 4,
	"rowSpan": 6
},
"metadata": {
	"inputs": [
	{
		"name": "queryInputs",
		"value": {
		"metrics": [
			{
			"resourceId": "/subscriptions/d1ecc7ac-c1d8-40dc-97d6-2507597e7404/resourcegroups/crumplinux-rg/providers/microsoft.compute/virtualmachines/crumplinux",
			"name": "Disk Read Bytes"
			},
...
```

<img style="border:3px solid #021a40" src="/files/azportal2.png">

Note the **colSpan** and **rowSpan** values here. 
{: .notice--info} 

You could edit this to change the **colSpan** and **rowSpan** to be a smaller tile by changing them to :

```json
 "colSpan": 2,
 "rowSpan": 2
```

Now save the file and upload it and you have your new tile:

<img style="border:3px solid #021a40" src="/files/azportal3.png">


Keep in mind that you can also do more sophisticated things such as use this to [programmatically](https://docs.microsoft.com/en-us/azure/azure-portal/azure-portal-dashboards-create-programmatically) create dashboards by using Azure Resource Manager APIs. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 