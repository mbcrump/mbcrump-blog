---
layout: post
title: "Azure Tips and Tricks Part 115 - Remove Azure Secrets committed to GitHub"
excerpt: "A tutorial on how to quickly remove Azure secrets committed to GitHub"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Tips and Tricks Videos are NOW Available!** : Get all the goodness of Azure Tips and Tricks in video form. [Read more about it here](http://www.michaelcrump.net/azure-tips-and-tricks106/)
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Remove Azure Secrets committed to GitHub

Writing code day after day means secrets, connection strings and more get added to your code. And if you are like me, they get committed to your GitHub database and then you are embarrassed. In this post, I'll walk you through cleaning up a repo. 

Part 1: 

* Change to the directory where you store your repo or clone a fresh copy with `git clone https://github.com/something/something.git`. 
* Clone a fresh copy of your repo using the mirror option, like the following `git clone --mirror https://github.com/something/something.git`. 
* You'll now have a bare repo. Below I've listed out the contents to verify. 

```text
Michaels-MBP:cleanme mbcrump$ ls -l
total 16
-rw-r--r--   1 mbcrump  staff  189 Apr 16 20:25 appsecrets.json
drwxr-xr-x  11 mbcrump  staff  352 Apr 16 20:26 cleanme.git
```

* You see that I have an appsecrets.json which contains some sensitive data that I need to remove: 

```text
{
  "ConnectionStrings": {
    "StorageAccountAPI": "DefaultEndpointsProtocol=https;AccountName=autotweet;AccountKey=+1234;EndpointSuffix=core.windows.net"
  }
}
```

Part 2:

* Install BFG with `brew install bfg` assuming you have Homebrew installed and using a Mac or [download](https://rtyley.github.io/bfg-repo-cleaner/) the JAR file if you are on Windows.

Part 3:

* Build a `passwords.txt` file and place and enter the passwords that you'd like to remove. 

Mine was replacing an Azure Storage Table key that I accidentally committed:

```text
DefaultEndpointsProtocol=https;AccountName=autotweet;AccountKey=+1234;EndpointSuffix=core.windows.net
```

Part 4:

* Run `bfg --replace-text passwords.txt cleanme.git`
* Below is output from that command:

```text
Cleaning
--------

Found 7 commits
Cleaning commits:       100% (7/7)
Cleaning commits completed in 253 ms.

Updating 1 Ref
--------------

	Ref                 Before     After   
	---------------------------------------
	refs/heads/master | 1aa1546d | 1aac2fd2

Updating references:    100% (1/1)
...Ref update completed in 89 ms.

Commit Tree-Dirt History
------------------------

	Earliest      Latest
	|                  |
	 .  D  m D  D  D  m 

	D = dirty commits (file tree fixed)
	m = modified commits (commit message or parents changed)
	. = clean commits (no changes to file tree)

	                        Before     After   
	-------------------------------------------
	First modified commit | 2b978e2d | 82b385c5
	Last dirty commit     | be1cde85 | 8ddbdf06

Changed files
-------------

	Filename          Before & After     
	-------------------------------------
	appsecrets.json | 5d8bfd89 ⇒ 21cdaeb1


In total, 10 object ids were changed. Full details are logged here:

	/Users/mbcrump/Documents/GitHub/cleanme/cleanme.git.bfg-report/2018-04-16/21-20-48
```

Part 5:

* Run `git reflog expire --expire=now --all && git gc --prune=now --aggressive`
* Run `git push` to push it to your repo.

Now if you go and look at your GitHub commit history, the password or sensitive data should be gone. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 