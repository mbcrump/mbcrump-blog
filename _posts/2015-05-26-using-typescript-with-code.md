---
layout: post
title: Using TypeScript with Visual Studio Code on OSX
excerpt: Follow this to get TypeScript working with Visual Studio Code on OSX
tags: blog
comments: true
---

Some of my other articles about Visual Studio Code : 

* [Using TypeScript with Visual Studio Code on OSX](http://michaelcrump.net/using-typescript-with-code/)
* [Setting up Github with Visual Studio Code on OSX](http://michaelcrump.net/using-github-with-visualstudio-code/)
* [Automatically Compile Your TypeScript Files with Visual Studio Code on OSX](http://michaelcrump.net/quick-tip-with-typescript-and-vscode/)
* [Creating and Debugging C# Console Apps with Visual Studio Code on OSX](http://michaelcrump.net/creating-and-debugging-console-apps-with-vscode/)

## Introduction

[Visual Studio Code](https://code.visualstudio.com/) is powerful editor that Microsoft released at Build 2015. There have been several questions regarding how to setup TypeScript with Visual Studio Code on OSX. I decided that I'd stop for a second and make a quick post showing you exactly how to do it. 

## Install TypeScript first

From your terminal, enter the following : 

	{% highlight text %}
	npm install -g typescript
	{% endhighlight %}	
	
You should see the following in your terminal window after running the command : 

	{% highlight text %}
$ npm install -g typescript
/usr/local/bin/tsc -> /usr/local/lib/node_modules/typescript/bin/tsc
/usr/local/bin/tsserver -> /usr/local/lib/node_modules/typescript/bin/tsserver
typescript@1.5.0-beta /usr/local/lib/node_modules/typescript
	{% endhighlight %}	

Notice that it installed typescript 1.5.0-beta. This is required for Visual Studio Code. 

## Switch Back to Visual Studio Code

Create a New Project and create a new file called tsconfig.json. 

{% highlight text %}
{
	"compilerOptions": {
		"target": "ES5",
		"module": "amd",
		"sourceMap": true
	}
}
{% endhighlight %}
	
Note: By default the target is ES3. I changed mine to ES5, which Visual Studio Code supports, but it also supports ES6 (experimental).

## Build the Project

If you press CMD-Shift-B, then it will ask you to configure the Task Runner. You will now have a file called tasks.json. Make sure it looks like the following: 

{% highlight text %}
{
	"version": "0.1.0",
	
	// The command is tsc.
	"command": "tsc",

	// Show the output window only if unrecognized errors occur. 
	"showOutput": "silent",
	
	// Under windows use tsc.exe. This ensures we don't need a shell.
	"windows": {
		"command": "tsc.exe"
	},
	
	// args is the HelloWorld program to compile.
	"args": [],
	
	"isShellCommand": true,
	
	// use the standard tsc problem matcher to find compile problems
	// in the output.
	"problemMatcher": "$tsc"
}
{% endhighlight %}
	
Note: Don't worry about the windows section as the OSX installation of Visual Studio Code will ignore it. The only thing we changed here was the **args** field, which allows it to compile all files in the current directory and subdirectory and added **isShellCommand** to true. Notice that under the **command** parameter, it has **tsc**. If you didn't install TypeScript first, then it would have failed here. 

## Create a main.ts file and add some TypeScript code

You can use the following sample code if you wish : 

{% highlight text %}
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

var greeter = new Greeter(" Twitter");

{% endhighlight %}
	
Press CMD-Shift-B and you should see a main.js has been created. 

> If you have any problems getting this to work, then check out my [Github repo](https://github.com/mbcrump/VSCodeSample) for this sample project.

Here is a screenshot of what Visual Studio Code looks like once complete : 

![image](/files/vscode052615.jpg)


## Wrap-up

Thanks for reading and if you have any questions or comments, then leave them below. 

