---
layout: post
title: Automatically Compile Your TypeScript Files with Visual Studio Code on OSX
excerpt: A quick and easy way to autocompile your TypeScript files with Visual Studio Code on OSX
tags: blog
comments: true
---

Some of my other articles about Visual Studio Code : 

* [Using TypeScript with Visual Studio Code on OSX](http://michaelcrump.net/using-typescript-with-code/)
* [Setting up Github with Visual Studio Code on OSX](http://michaelcrump.net/using-github-with-visualstudio-code/)
* [Automatically Compile Your TypeScript Files with Visual Studio Code on OSX](http://michaelcrump.net/quick-tip-with-typescript-and-vscode/)
* [Creating and Debugging C# Console Apps with Visual Studio Code on OSX](http://michaelcrump.net/creating-and-debugging-console-apps-with-vscode/)

## Introduction

I've been using [Visual Studio Code](https://code.visualstudio.com/) since it was released at Build 2015. As I've been using this powerful editor, I've come across a couple of ways to make it even better and I thought I'd share it with the community. In this post, we are going to make our .ts (TypeScript) files auto-compile instead of performing the **Build** command every time we make changes to our .ts files. 

Before we get started, simply follow [this post](http://michaelcrump.net/using-typescript-with-code/) and make sure TypeScript is installed and working. 

## Split-Screen FTW

We are going to use the split-screen functionality of Visual Studio Code in order to see both of our TypeScript and generated JavaScript file. Simply press the button highlighted below or press CMD-\ : 

![image](/files/splitscreenvscode.jpg)

Put your TypeScript file that you are currently working on in the left panel and the generated JavaScript file in the right panel. Notice that if you make a change to the TypeScript file, the JavaScript file is not updating. You will need to press the CMD-Shift-B in order to compile the file. EVERY. SINGLE. TIME. 

![image](/files/tscnotautocompiling.gif)

## A Little Help from TSC

Navigate to your Visual Studio Code Folder and open a terminal window here and enter the following command:

{% highlight text %}
tsc *.ts --watch
{% endhighlight %}
	
This is going to monitor the folder for any changes in our TypeScript files and compile them behind the scenes. Here is what the output looks like once you start it: 

{% highlight text %}
message TS6042: Compilation complete. Watching for file changes.
message TS6032: File change detected. Starting incremental compilation...
message TS6042: Compilation complete. Watching for file changes.
{% endhighlight %}

 
## Switch Back to Visual Studio Code

If you were already in the split-screen mode, then you should have noticed the change in your JavaScript file already. As you begin typing, it will automatically compile your TypeScript file as shown below. 

![image](/files/tscautocompiling.gif)

>Note: Since this is a Node app, Control-C will kill the process in the terminal window if you want to stop tsc from watching for file changes. 

## Like this Post?

Thanks for reading and if you like this post, then share it with one of the buttons below. Also, feel free to leave a comment below. 

