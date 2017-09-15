---
layout: post
title: Unable to Activate Windows Store App 
excerpt: 
tags: blog
comments: true
---


### Introduction

I’ve recently been working on several HTML applications and sharing the code through DropBox through my various machines. (Yes I have TFS – but this is sample code). One problem that I’ve experienced is that sharing the code on different machines will result in the following error when the app is launched.

[![](http://michaelcrump.net/files/SNAGHTML802876c_thumb_634844172152882324.png "SNAGHTML802876c")](http://michaelcrump.net/files/SNAGHTML802876c_634844172142586324.png)

**Unable to Activate Windows Store App. The activation request failed with error ‘E_Fail’. See help for advice on troubleshooting the issue.**

### The Fix

The easiest way to get back to work is to select “**Show All Files**” then expand **<u>bin</u>** and **<u>bld</u>** and delete the **Debug** Folder in each. After that is complete the app will launch again. See the diagram below for more info. 

_Note: The Debug folders will be recreated automatically._

[![image](http://michaelcrump.net/files/image_thumb_634844173774190324.png "image")](http://michaelcrump.net/files/image_634844173761554324.png)

### Wrap-Up

Anyways I hope this helps someone with a similar problem. I created this blog partially for myself but it is always nice to help my fellow developer.

Thanks for reading.