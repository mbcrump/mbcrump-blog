---
layout: post
title: "Day 1 - Installing and Running .NET Core on a Windows Box"
excerpt: "Learn how to work with .NET Core in this mini-series"
tags: [edge, windows, chrome, aspnet, dotnetcore, uwp]
share: true
comments: true
---

Disclaimer: *I am **not** on the .NET Core Team*. I used the tools available publicly.

## Intro

A complete list of post in this series is included below :

* [Day 1 - Installing and Running .NET Core on a Windows Box](http://michaelcrump.net/getting-started-with-aspnetcore/)
* [Day 2 - Taking a Look at the Visual Studio Templates for .NET Core](http://michaelcrump.net/part2-aspnetcore/)
* [Day 3 - Running a .NET Core app on a Mac](http://michaelcrump.net/part3-aspnetcore/)
* [Day 4 - Creating a NuGet Package from .NET Core app](http://michaelcrump.net/part4-aspnetcore/)
* [Day 5 - Creating a Test Project from .NET Core](http://michaelcrump.net/part5-aspnetcore/)
* [Day 6 - Migrating an existing .NET Core to csproj](http://michaelcrump.net/part6-aspnetcore/)
* [Day 7 - Creating an ASP.NET Core Web Application](http://michaelcrump.net/part7-aspnetcore/)
* [Day 8 - Using Visual Studio Code with a .NET Core Console Application](http://michaelcrump.net/part8-aspnetcore/)
* [Day 9 - Creating a .NET Core Console App inside of Visual Studio Code](http://michaelcrump.net/part9-aspnetcore/)
* [Day 10 - Using JetBrains Rider with a .NET Core Console Application](http://michaelcrump.net/part10-aspnetcore/)

In this mini-series, I plan to walk you through [.NET Core](https://www.microsoft.com/net/core) as I learn it. In short, .NET Core runs on Windows, Mac and a couple of distros of Linux. It supports several languages (like C#) and is [open-source](https://github.com/dotnet/core). If you want to learn more about the differences between .NET Core and the .NET Framework, then I would suggest reading this [post](https://docs.microsoft.com/en-us/dotnet/articles/standard/choosing-core-framework-server). 

## Installing it

There is a couple of things that might help with installing it. On the [downloads page](https://www.microsoft.com/net/download/core), you will see two options and may not know which one to select. The key takeaway here is that one is for creating and the other is just for running .NET Core apps on a machine : 

* .NET Core 1.0.3 SDK - Installer (Includes the tools for **creating** .NET Core apps)
* .NET Core 1.0.3 SDK - Binaries Only (Only Includes the ability to **run** .NET Core apps)

You will want to take the "Installer option" for this guide as we will be creating .NET Core apps.

You will also want the option to install .NET Tools for Visual Studio. This will allow us to create a new VS Project using a template. Keep in mind that this only works with Visual Studio 2015 or 2017. 

To recap, you installed the following items (depending on your VS version and architecture ) : 

![image](/files/installercore.png)

## Verifying Installation

You can easily verify it was installed properly by opening a command prompt and typing: 

	dotnet 

You should see the following : 

![image](/files/dotnetcoreinstalled.png)

You can test that it was installed in Visual Studio by going to "Help" and "About" as shown below and looking for Microsoft .NET Core Tools. 

![image](/files/dotnetcorevs.png)

While you are here you can go to File->New Project and look for .NET Core to create a project in Visual Studio.

![image](/files/dotnetcorevstemplates.png)

## Kick the tires

I'd suggest starting with the command prompt and typing : 

	dotnet help

You will see that it list the common commands : 

	new           Initialize a basic .NET project
	restore       Restore dependencies specified in the .NET project
	build         Builds a .NET project
	publish       Publishes a .NET project for deployment (including the runtime)
	run           Compiles and immediately executes a .NET project
	test          Runs unit tests using the test runner specified in the project
	pack          Creates a NuGet package

Begin with the command : 

	dotnet new --help

and you will see the following : 
	
	Options
	  -h|--help             Show help information
	  -l|--lang <LANGUAGE>  Language of project [C#|F#]
	  -t|--type <TYPE>      Type of project

At this point I'm not sure what types are available so I tried : 

	dotnet new -t blah

And it listed the available projects which included Console, Web, Lib and xunittest.

To create a new console app, I typed

	dotnet new -t console

If I didn't specify it then it would have created a console app anyways, but we need to get into the habit of specifying the type. I now have a Program.cs file and a .json file. If I examine the Program.cs, then it has the following code:

	using System;
	
	namespace ConsoleApplication
	{
	    public class Program
	    {
	        public static void Main(string[] args)
	        {
	            Console.WriteLine("Hello World!");
	        }
	    }
	}

You can modify the code or leave it as is. I'm going to leave it as is. 

Now we need to restore the packages (dependencies) by using `dotnet restore` and we can build it with `dotnet build`. 

Now we need to run it. So I typed `dotnet run` and the application returned the following:

	C:\Users\mbcrump\helloworld>dotnet run
	Project helloworld (.NETCoreApp,Version=v1.0) was previously compiled. Skipping compilation.
	Hello World!

Yeah, we now see our output from the Program.cs file. 

## Wrap-up

That's it for now. As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below if there is something that you want to know as I learn .NET Core.