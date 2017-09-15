---
layout: post
title: "Day 4 - Exploring Docker for Windows - Running Docker Documentation Locally"
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

## Searching Docker Images

Whenever you need to search for a Docker image, the first place that you may think of is heading over to docker.com. But a much more easier way is through the command line. Simply type : 

	docker search searchterm

You can also use quotes if you need to search something that has a space in between it. (ex. Docker documentation)

	docker search "docker documentation"

Below is a snippet of you can expect : 

	C:\Users\mbcru>docker search "docker documentation"
	NAME                                    DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
	docker                                  Docker in Docker!                               439       [OK]
	konradkleine/docker-registry-frontend   Browse and modify your Docker registry in ...   143                  [OK]
	plexinc/pms-docker                      Official Plex Media Server Docker Repo          85                   [OK]
	docker-dev                              Docker is an open source project to pack, ...   63        [OK]
	datadog/docker-dd-agent                 Docker container for the Datadog Agent.         50                   [OK]
	francescou/docker-compose-ui            web interface for Docker Compose                41                   [OK]
	docker/docker-bench-security            Docker Bench checks for dozens of common b...   20                   [OK]
	dockercore/docker                                                                       18                   [OK]
	laurentmalvert/docker-boinc             A dockerized BOINC client                       12                   [OK]
	runmymind/docker-android-sdk            docker-android-sdk                              10                   [OK]
	sematext/sematext-agent-docker          Performance Monitoring, Events and Logs fo...   8                    [OK]
	docs/docker.github.io                   Builds of the Docker documentation              6                    [OK]
	fabric8/jenkins-docker                  Fabric8 Jenkins Docker Image                    4                    [OK]
	docker/migrator                         Tool to migrate Docker images from a v1 re...   4                    [OK]

You can now use the `docker run name` to download the container. (You may have to switch to Linux containers). 

## Downloading Docker documentation and running it locally

This is something that I really enjoy doing with documentation and that is having a local copy on my hard drive. You can do it fairly easily by using the search command as shown earlier. 

You can download it with the following command : 

	docker run docs/docker.github.io

When it is finished you will see a URL at the bottom where you can view the documentation locally : 

	C:\Users\mbcru>docker run docs/docker.github.io
	Unable to find image 'docs/docker.github.io:latest' locally
	latest: Pulling from docs/docker.github.io
	75a822cd7888: Pull complete
	57de64c72267: Pull complete
	4306be1e8943: Pull complete
	871436ab7225: Pull complete
	afb684ad7765: Pull complete
	0d97dae2054f: Pull complete
	81cf204ae25e: Pull complete
	b2c097f43e0f: Pull complete
	77fb0c414503: Pull complete
	5ce98315c3d9: Pull complete
	4fb049720eda: Pull complete
	1a395df07195: Pull complete
	11870ae3ca13: Pull complete
	0c32f21045f7: Pull complete
	30ecf115ebb4: Pull complete
	c89fc62f83bc: Pull complete
	a15c2890523d: Pull complete
	3bfc5dc19752: Pull complete
	0c54303cb6ba: Pull complete
	Digest: sha256:297a70ae474216eab46c1c19f884263fba91b6a198d54383d421d0bbf37aecda
	Status: Downloaded newer image for docs/docker.github.io:latest
	Docker docs are viewable at:
	http://0.0.0.0:4000

Open a web browser and navigate to http://localhost:4000/. You should see the documentation. It is an exact duplicate of docs.docker.com. Cool!

![image](/files/dockerlocally.png)


## Wrap-up

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 
