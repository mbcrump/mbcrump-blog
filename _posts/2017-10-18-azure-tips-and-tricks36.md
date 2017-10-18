---
layout: post
title: "Azure Tips and Tricks Part 36 - Quickly Renew or Revoke Azure Functions Keys"
excerpt: "Learn how to quickly renew or revok Azure Functions keys using the Azure Portal"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Quickly Renew or Revoke Azure Functions Keys

There are times when you've created a new Azure Function HTTP Trigger where your Function Key needs to be changed. For example, here is my Function URL: 

<img style="border:3px solid #021a40" src="/files/funckey1.png">

`https://mynewtestapp100.azurewebsites.net/api/HttpTriggerCSharp1?code=FJmHHtDmvqwp4wn0zXCS9J70NbakcmNDYCwM6trPOCTK3TdiCVg8pA==`

If you go to that page, you'll see the Trigger was activated as you passed the key: 

```text
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">
Please pass a name on the query string or in the request body
</string>
```

If something happens and someone gets the key, then you should go back to your Function and click **Manage**, then press **Revoke**. Now you can quickly gneerate a new key with the **Add new function key**. You'll need to provide the name **default** and can leave the value empty. Now simply click **Save** and if you go back to  your Function and click on **Get Function URL**, then you'll notice the new key is in place. 

<img style="border:3px solid #021a40" src="/files/funckey2.png">

Now I need to go and revoke my key again! Durn it!

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--inverse} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 