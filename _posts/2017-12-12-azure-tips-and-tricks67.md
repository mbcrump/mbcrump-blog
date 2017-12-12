---
layout: post
title: "Azure Tips and Tricks Part 67 - Querying documents properties with special characters in Cosmos DB"
excerpt: "Learn how to query documents properties with special characters in Cosmos DB"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Querying documents properties with special characters in Cosmos DB

I was working with Cosmos DB yesterday and hit the following snag that I couldn't query my document that had special characters in it. Such is an example: 

<img style="border:3px solid #021a40" src="/files/querycosmos1.png">

Notice the `"$type": "mytype",` has a `$` in it. 

If you head over to **Query Explorer** and try to query it using...

```text
SELECT * 
FROM testing t
WHERE t.$type = 'mytype'
```

... then you'll see the following error: 

<img style="border:3px solid #021a40" src="/files/querycosmos2.png">

I was able to fix this by wrapping the property inside `[]` such as...

```text
SELECT * 
FROM testing t
WHERE t["$type"] = 'mytype'
```

Now my query returned properly

<img style="border:3px solid #021a40" src="/files/querycosmos3.png">

Not sure if this helps anyone, but worth flagging. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 