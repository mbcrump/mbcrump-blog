---
layout: post
title: "Day 1 - Exploring Docker for Windows - Getting Started"
excerpt: "Learn how to get started working with Docker in this series"
tags: [docker, windows, edge, dotnet, dotnetcore, web]
share: true
comments: true
---

## Intro

In this mini-series, I plan to walk you through [Docker](https://www.docker.com) as I learn it. In short, Docker is an open-source project that automates the deployment of applications inside software containers. For developers, I think it can be summarized with one sentence. Docker automates the repetitive tasks of setting up and configuring development environments so that developers can focus on what matters: building great software. I would recommend reading this [post](https://www.docker.com/what-docker) to learn exactly what Docker is in their own words. 


A complete list of post in this series is included below :

* [Day 1 - Exploring Docker for Windows - Getting Started](http://michaelcrump.net/part1-docker/)
* [Day 2 - Exploring Docker for Windows - Stopping and Restarting Containers](http://michaelcrump.net/part2-docker/)
* [Day 3 - Exploring Docker for Windows - Removing Containers and Images](http://michaelcrump.net/part3-docker/)
* [Day 4 - Exploring Docker for Windows - Running Docker Documentation Locally](http://michaelcrump.net/part4-docker/)
* [Day 5 - Exploring Docker for Windows - Running A Command Prompt Inside a Container](http://michaelcrump.net/part5-docker/)
* [Day 6 - Exploring Docker for Windows - Accessing Files inside a Container](http://michaelcrump.net/part6-docker/)

## Installing it

There is a couple of things that might help with installing it. On the [downloads page](https://www.docker.com/docker-windows), you will want to download the community edition. You will see two channels. 


- Stable channel - The Stable version comes with the latest GA release of Docker Engine	
- Edge channel - The Edge version offers access to cutting edge features

You will want to take the "Stable channel" for this guide as we want to learn on stable builds. Let the installer run as shown below: 

![image](/files/installerdocker.png)

As it is installing, it will automatically prompt you to turn on Hyper-V (if not already on) and reboot. 

## Verifying Installation

You can easily verify it was installed properly by opening a command prompt and typing: 

	docker info

You should see the following : 

![image](/files/dockercl.png)

Now is also a good time to switch to "Windows Containers" as we are about to install mongogb. Go ahead and look for Docker in your task bar and right click it and select "Switch to Windows Containers" as shown below. 

![image](/files/dockerwincontain.png)

## Start working with mongodb 

Since I want to work with mongodb. I simply searched for `mongodb docker` and found the following [page](https://hub.docker.com/_/mongo/). After reading the page, I started with the following command : 

	docker run mongo:windowsservercore

You will see the following output after it completes that shows it downloaded it successfully and started the database (I trimmed the output below) : 

	Unable to find image 'mongo:windowsservercore' locally
	windowsservercore: Pulling from library/mongo
	3889bb8d808b: Pull complete
	3430754e4d17: Pull complete
	e9d9d048a108: Pull complete
	cddb40b56537: Pull complete
	bd302c5a9bef: Pull complete
	7727ae324d45: Pull complete
	1fc790f6d18c: Pull complete
	3ed22695a264: Pull complete
	1a0e773c199f: Pull complete
	dadec33a3190: Pull complete
	Digest: sha256:90d80c5fdc534118c476edf158ce1d814325b2e6300a8573d7e1c2c2a8ad8b4a
	Status: Downloaded newer image for mongo:windowsservercore

Open another command prompt (think of this one as the client) and type the following : 

	docker ps

and it will list available containers :

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS               NAMES
	8fdada2313be        mongo:windowsservercore   "mongod"            About an hour ago   Up About an hour    27017/tcp           sharp_mirzakhani

Take note of the name (listed at the end of the previous command) and pass it into the command below :  

	docker exec -it sharp_mirzakhani mongo

This will start our Docker instance as shown below : 

	MongoDB shell version v3.4.1
	connecting to: mongodb://127.0.0.1:27017
	MongoDB server version: 3.4.1
	Welcome to the MongoDB shell.
	For interactive help, type "help".
	For more comprehensive documentation, see
	        http://docs.mongodb.org/
	Questions? Try the support group
	        http://groups.google.com/group/mongodb-user
	2017-03-18T11:51:34.655-0700 I STORAGE  [main] In File::open(), CreateFileW for '' failed with The system cannot find the path specified.
	Server has startup warnings:
	2017-03-18T10:52:22.711-0700 I CONTROL  [initandlisten]
	2017-03-18T10:52:22.711-0700 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
	2017-03-18T10:52:22.711-0700 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
	2017-03-18T10:52:22.711-0700 I CONTROL  [initandlisten]

Cool! We have an instance of mongodb running! You can even type `show dbs` to see the local database. 

**Note:** Keep in mind that the database isn't secure as you see all the warning messages. In other words, don't use this in production. 


## Wrap-up

This is very cool! I setup a mongodb server in just a couple of steps! I'm starting to like Docker. As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
