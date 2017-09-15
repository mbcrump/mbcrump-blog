---
layout: post
title: "Day 2 - Exploring Docker for Windows - Stopping and Restarting Containers"
excerpt: "Learn how to start and stop containers in Docker"
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

## Working with mongodb 

To recap, we learned how to run Mongodb with the following command : 

	docker run mongo:windowsservercore

We saw that it downloaded and started the database and we used `docker ps` to see our existing containers :

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS               NAMES
	8fdada2313be        mongo:windowsservercore   "mongod"            About an hour ago   Up About an hour    27017/tcp           sharp_mirzakhani

We then passed the following command to start our Docker instance and noticed that it attached to our running server :  

	docker exec -it sharp_mirzakhani mongo

It was very easy to get this up and running and we are starting to learn the power of working with Docker. 

## Stopping our running container

Run the `docker ps` and notice the output : 

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS              PORTS               NAMES
	8fdada2313be        mongo:windowsservercore   "mongod"            About an hour ago   Up About an hour    27017/tcp           sharp_mirzakhani

Now take the container id and type the first few letters of it as shown below : 

	docker stop 8fd

It will automatically find the container that matches the name and stop it. 

## Restarting a container

Just like software, it doesn't uninstall the software if we stop or start it. We will begin with `docker ps -a` to see all of our existing containers (starting or stopped).

	CONTAINER ID        IMAGE                     COMMAND             CREATED             STATUS                           PORTS               NAMES
	08d1b4b2cb7f        mongo:windowsservercore   "mongod"            6 minutes ago       Up 6 minutes                     27017/tcp           frosty_stallman
	6d1b71d8fb45        mongo:windowsservercore   "mongod"            7 minutes ago       Exited (1067) 4 minutes ago                          hardcore_swanson
	8fdada2313be        mongo:windowsservercore   "mongod"            8 days ago          Exited (2147483648) 7 days ago   27017/tcp           sharp_mirzakhani

We don't have to use the run command as we did in the last post. We can now restart a container that has been stopped with using the following command with the first few letters of the container id : 

	docker start 8df

Again, it will automatically find the container that matches the name and stop it. 

## Wrap-up

It is important to grasp this concept of restarting and stopping container as we'll learn how to remove containers and images in the next section. As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
