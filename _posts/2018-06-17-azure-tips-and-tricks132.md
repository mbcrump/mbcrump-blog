---
layout: post
title: "Azure Tips and Tricks Part 132 - Increase the timeout of ASP.NET Core 2.0 API hosted in Azure App Service"
excerpt: "Learn how to quickly increase the timeout of ASP.NET Core 2.0 API hosted in Azure App Service"
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

## Increase the timeout of ASP.NET Core 2.0 API hosted in Azure App Service

There are reasons that you **might** have a request that takes 2-3 minutes to complete and this post is for you. For most, you should probably look at decoupling these long running request. 

If you're using ASP.NET Core 2.0 API and deploying to an Azure App Service, then you might run into an issue where it takes a process request longer than 2 minutes to complete. You'll typically get a `502 Bad Gateway` with the following info:

`"The specified CGI application encountered an error and the server terminated the process".`

If you check your diagnostic logfile you might see:

```
018-06-15 03:47:03.232 +00:00 [Error] Microsoft.AspNetCore.Diagnostics.DeveloperExceptionPageMiddleware: An unhandled exception has occurred while executing the request
System.Threading.Tasks.TaskCanceledException: A task was canceled.
```

You can fix this by going into your web.config in your sites/wwwroot folder and adding a `requestTimeout="00:20:00` to the file as shown below.

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.webServer>
    <handlers>
      <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModule" resourceType="Unspecified" />
    </handlers>
    <aspNetCore processPath="dotnet" arguments=".\WebApplication1.dll" stdoutLogEnabled="false" stdoutLogFile=".\logs\stdout" requestTimeout="00:20:00" />
  </system.webServer>
</configuration>
<!--ProjectGuid: 3b93921c-f843-46c8-914e-xxx-->
```

For more details, read the [ASP.NET Core Module configuration reference](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-2.0#attributes-of-the-aspnetcore-element) on Microsoft Docs. 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 