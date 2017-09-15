---
layout: post
title: "Day 5 - Exploring Docker for Windows - Running A Command Prompt Inside a Container"
excerpt: "Learn how to run a copy of the docker documentation locally"
tags: [docker, windows, edge, dotnet, dotnetcore, web]
share: true
comments: true
---

## Intro

In this mini-series, I plan to walk you through [Docker](https://www.docker.com) as I learn it. 

A complete list of post in this series is included below :

* [Day 1 - Exploring Docker for Windows - Getting Started](http://michaelcrump.net/part1-docker/)
* [Day 2 - Exploring Docker for Windows - Stopping and Restarting Containers](http://michaelcrump.net/part2-docker/)
* [Day 3 - Exploring Docker for Windows - Removing Containers and Images](http://michaelcrump.net/part3-docker/)
* [Day 4 - Exploring Docker for Windows - Running Docker Documentation Locally](http://michaelcrump.net/part4-docker/)
* [Day 5 - Exploring Docker for Windows - Running A Command Prompt Inside a Container](http://michaelcrump.net/part5-docker/)
* [Day 6 - Exploring Docker for Windows - Accessing Files inside a Container](http://michaelcrump.net/part6-docker/)

## Running an interactive application inside a container

We've ran a couple of applications that run in the background, but haven't yet tried running an application that we'll interact with. I think a good example of this is running .NET Core in the Command Prompt. Let's Begin :

If you navigate to [https://hub.docker.com/r/microsoft/dotnet/](https://hub.docker.com/r/microsoft/dotnet/) in your web browser, you will see is an image for .NET Core to run inside of Docker. 

Begin by typing the following command via PowerShell : 

	docker run microsoft/dotnet:nanoserver

And you'll see it pull down the image and try to run it as shown below : 

	PS C:\Windows\system32> docker run -it microsoft/dotnet:nanoserver
	Unable to find image 'microsoft/dotnet:nanoserver' locally
	nanoserver: Pulling from microsoft/dotnet
	bce2fbc256ea: Downloading [>                                                  ] 1.065 MB/252.7 MB
	58f68fa0ceda: Downloading [===>                                               ] 8.093 MB/114.9 MB
	67bce391bf48: Download complete
	d50d4762f91f: Download complete
	057903a00c7c: Download complete
	f2c2ae47c5db: Downloading [======================>                            ] 55.69 MB/125.5 MB
	54e60e47aa5f: Waiting
	41b108ae93d3: Waiting
	d1e8a8809606: Waiting
	Microsoft Windows [Version 10.0.14393]
	(c) 2016 Microsoft Corporation. All rights reserved.
	
	C:\>

You see that it listed the C Prompt but you can't type anything. 

If you run `docker ps -a` then you will see a list of processes (stop or started) :

	CONTAINER ID        IMAGE                         COMMAND                    CREATED              STATUS
	                   PORTS               NAMES
	0bd91d15c075        microsoft/dotnet:nanoserver   "c:\\windows\\system..."   About a minute ago   Exited (0) About a min
	ute ago                                clever_shirley

We can see that it started our instance of .NET Core but it exited out. We can't see the command that it ran as it truncated it from the output. To fix that, we need to run `docker ps -a --no-trunc` to see what command was actually executed : 

	CONTAINER ID                                                       IMAGE                         COMMAND                            CREATED             STATUS
	                       PORTS               NAMES
	0bd91d15c075ce09896cce6c129919570c4983543085674eaa0114d5eadf7142   microsoft/dotnet:nanoserver   "c:\\windows\\system32\\cmd.exe"   4 minutes ago       Exited (0) 4
	minutes ago                                clever_shirley

We can now see that it started `c:\\windows\\system32\\cmd.exe`. Great! So this is a command prompt that we are looking for. OK, so let's go ahead and run the docker run command and add -it for Interactive Terminal :

	docker run -it microsoft/dotnet:nanoserver

Now we are running a command prompt inside of a Container using Docker. We can even run `dotnet --info` to verify. 

![image](/files/dockerdotnet.png)

You can type `exit` to return to PowerShell on your local machine. Very cool!


## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
