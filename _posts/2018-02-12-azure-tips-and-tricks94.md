---
layout: post
title: "Azure Tips and Tricks Part 94 - Customize an Azure Functions Endpoint in Seconds"
excerpt: "Learn how to query an Azure Search Index using C#"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Customize the Azure Functions endpoint

This one tends to come up a lot and typically folks want to solve the following two problems. 

* They want to know know how to pass a string parameter to the functions URL.
* Then parse the string from the URL and use it in my code logic.

They basically want a url like the following - https://mcrumpfunction.azurewebsites.net/api/products/truck/444

You can achieve this by going into your Azure Function and looking at your **function.json** file and adding the route. More than likely **route** is missing, but you can easily add it. 

Below is a sample that looks for the word products in the string followed by a category that is alphanumeric and an id that is an integer:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "name": "req",
      "direction": "in",
      "methods": [
        "get"
      ],
      "route": "products/{category:alpha}/{id:int?}"
    },
    {
      "name": "$return",
      "type": "http",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Now we'll add the two values (`string category, int? id`) to pass into our method as shown below.

```csharp
using System.Net;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, TraceWriter log)
{
    log.Info("C# HTTP trigger function processed a request.");

    return category == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a category")
        : req.CreateResponse(HttpStatusCode.OK, "Category " + category + " and the Id is " + id);
}
```

If you now call `https://mcrumpfunction.azurewebsites.net/api/products/truck/444` then it will return `<string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Category truck and the Id is 444</string>`. 

Very simple!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 