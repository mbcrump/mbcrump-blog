---
layout: post
title: New Blog Launched
excerpt: Details on my new blog that I recently launched
tags: blog
comments: true
---

## FunnelWeb


I've used [FunnelWeb](http://www.funnelweblog.com/) for the past couple of years and decided that it is time to move on. Since Funnelweb is open-source and based off of MVC 3, I jumped on the bandwagon and customized it to my liking. The problem is that the project has grown stale and almost all of the original developers have moved on. It also has a lot of problems with modern web and mobile browsers just to name a few. It looked like this in a browser. 

![image](/files/funnelweb.png)

*Not so great, I know*

## Moving On

After evaluating different blog engines, I decided that my requirements were the following:

* Needs to look great on modern web and mobile browsers. 
* I wanted a blog that didn't rely on a database. (SQL Server was required for FunnelWeb)
* I needed a better comment system instead of using the one built-into FunnelWeb. 
* I didn't want the bloat of some of the popular blog engines. 
* I wanted to write using MarkDown.
* It needed to have great syntax highlighting support for a variety of programming languages. 
* Just a few HTTP request per page load. 

## What I Decided

I went with [Jekyll](http://jekyllrb.com/) as it met all of my requirements and I'm able to install it on my GitHub page and get a lightning fast host for free. 

![image](/files/jekyllblogmc.png)

## The Challenges

My first challenge was moving all the content out of FunnelWeb. FunnelWeb uses SQL Server, so I was able to simply log in and write a custom SQL Query to return only the data that I needed. I then saved it as a CSV file. Next, I needed to parse the CSV file and output files in a format that Jekyll can use. I quickly opened Visual Studio and wrote a C# program to do this. Once I had all of the files, I downloaded all the images and uploaded them to my site. I still had some formatting issues that my friend, [Brian Rinaldi](https://twitter.com/remotesynth) helped me solve. 

## Still a Work in Progress

Even though my new blog has launched, I already have several things in mind that I want to tweak and content that I want to add. Thankfully, the sky is the limit as far as customizing it. Anyways, thanks for reading!

