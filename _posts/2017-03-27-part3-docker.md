---
layout: post
title: "Day 3 - Exploring Docker for Windows - Removing Containers and Images"
excerpt: "Learn how to remove containers and images in Docker"
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

## Removing containers

Think of **removing containers** as **uninstalling software**. If you have an application on your machine and you uninstall it, then the application will not be running or on your hard disk. But the installation (.msi, etc) will still be on your system (which we'll cover). 

Begin by running `docker ps -a` to see all of our existing containers (starting or stopped).

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                           PORTS               NAMES
	08d1b4b2cb7f        mongo:windowsservercore   "mongod"            6 minutes ago       Up 6 minutes                     27017/tcp           frosty_stallman
	6d1b71d8fb45        mongo:windowsservercore   "mongod"            7 minutes ago       Exited (1067) 4 minutes ago                          hardcore_swanson
	8fdada2313be        mongo:windowsservercore   "mongod"            8 days ago          Exited (2147483648) 7 days ago   27017/tcp           sharp_mirzakhani

Run the following (assuming the last part is the first three letters of the container ID) : 

	docker rm 8fd

Run `docker ps -a` and you'll see it has been removed. 

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                           PORTS               NAMES
	08d1b4b2cb7f        mongo:windowsservercore   "mongod"            6 minutes ago       Up 6 minutes                     27017/tcp           frosty_stallman
	6d1b71d8fb45        mongo:windowsservercore   "mongod"            7 minutes ago       Exited (1067) 4 minutes ago                          hardcore_swanson

## Removing images

Think of **removing images** as **deleting an installer**. If you have an application on your machine and you uninstall it, then the application will not be running or on your hard disk. But the installation (.msi, etc) will still be on your system. Now we'll learn how to delete it. Begin with the following to list all of your Docker images that have been downloaded : 

	docker images

You will see the following : 

	REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	mongo               windowsservercore   ce615778458a        7 weeks ago         9.77 GB

Now run the following command and it will delete the repository.  : 

	docker rmi ce6

Notice the output below and that it is actually deleting the image that you downloaded : 

	C:\Users\mmcru>docker rmi ce6
	Untagged: mongo:windowsservercore
	Untagged: mongo@sha256:90d80c5fdc534118c476edf158ce1d814325b2e6300a8573d7e1c2c2a8ad8b4a
	Deleted: sha256:ce615778458a1fc587ba51e920671cbacf7368a70d6104d549d8988fb1790070
	Deleted: sha256:f22f0d7ea4488f027a2e807c774a40dd6fd4b880e25ad7bd54372a1467f8f3e7
	Deleted: sha256:897d44b14f3d5586d56728bba5cf1e685c2617caa80b46fba049b9e28150b29e
	Deleted: sha256:dc65c961c5f7a2ce21f27df11b5fbe4fa6dacdd8f71b7ff33d3c192e75abebcb
	Deleted: sha256:10191ddea8998be762b0d458d7a4022dc163c2700797744cecdf8918e128f09c
	Deleted: sha256:a231cf36dbe2c5ce8ff9eb8fa19eed99dc835d695269751871fc3d7e973c2a17
	Deleted: sha256:917dfea9ff3ee69ea077fc2c04d122ea9137f9cb909c798ab8d9eee62206f546
	Deleted: sha256:4f65f64627ffa001f52a02f1088be466a49ba8f18905f03c7b63b8fae381c63a
	Deleted: sha256:f42f69dbf0fff4a6afa9d10059140477710ea237f587ac6bec2656d19bee12f9
	Deleted: sha256:f8a4522a02b230a736868a95205a455435a30b23c9c456492f905db2dc58f101
	Deleted: sha256:f358be10862ccbc329638b9e10b3d497dd7cd28b0e8c7931b4a545c88d7f7cd6

## Wrap-up

This is another key part of understanding Docker and using it to it's fullest. As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
