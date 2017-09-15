---
layout: post
title: "Day 8 - Using Visual Studio Code with a .NET Core Console Application"
excerpt: "Learn how to use Visual Studio Code with a .NET Core Console application"
tags: [edge, windows, chrome, aspnet, dotnetcore, web]
share: true
comments: true
---

Disclaimer: *I am **not** on the .NET Core Team*. I used the tools available publicly and have no insights into the future of .NET Core. It looks very bright though. :)

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

In this post, we're going to look at how you can use Visual Studio Code with a .NET Core Console application. 

## Install Visual Studio Code 

Before we do anything, make sure that you have installed Visual Studio Code. If you haven't downloaded it before, then you can find it [here](https://code.visualstudio.com/). After it is installed, your powerful new editor is ready to go: 

![image](/files/vscodeinstall.png)

Launch VS Code Quick Open by pressing (Ctrl+P) and paste `ext install csharp`. Take the first option as highlighted below: 

![image](/files/cscodecsharpext.png)

I typically hit the `reload` button afterwards to make sure that it took. 

## Back to the Command Prompt

***Note**: I'm using the latest RC of .NET Core and YES, I'm very aware that you can create a .NET Core Console app inside of VS Code. Maybe a post for another day?*

To create a new console app, I typed

	dotnet new console

If I didn't specify it then it would have created a console app anyways (in the current LTS), but we need to get into the habit of specifying the type as it may change.

Restore the packages by typing `dotnet restore` and build it with `dotnet build`. 

Run the app with `dotnet run` (again nothing new here) and you'll see the following:

	C:\Users\mbcrump\helloworld>dotnet run
	Hello World!

If you examine the Program.cs file, then it has the following code:

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

Just keep in mind here that it displays "Hello World".

**Pro tip:** You can open files directly in VS Code from the command prompt with `code filename.cs`. 

## Inside of Visual Studio Code

Switch back over to Visual Studio Code and open the folder of the Console app that you just created. 

You will be prompted of a warning and missing assets. Make sure that you `yes` and restore as shown below: 

![image](/files/vscoderestoreassets.png)

Click on the Debug icon, and make sure `.NET Core Launch` is selected and hit the run button. You should be able to see in the Debug Console the result of your console app. 

![image](/files/apprunningvscode.png)

*Ignore the errors in this screenshot as I've been putting .NET Core through the ringer :)*

## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 