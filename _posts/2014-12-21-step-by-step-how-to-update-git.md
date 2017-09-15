---
layout: post
title: "Step-by-Step on How to Update Git on Mac"
excerpt: "A quick way to update your Git client to the official distro."
tags: [git, mac, sourcecontrol]
comments: true
---

### Introduction

I've seen a lot of questions on the web about how to update your Mac client to the latest version which contains the fix for the security vulnerability announced last week. 
<br><br>
It is actually quite simple:<br>
<br>
Open your terminal prompt and type the following: 
	{% highlight text %}
	git --version
	{% endhighlight %}
If it comes back with the following result, then you are using Apple's Git, not the offiical distro of Git. 
	{% highlight text %}
	git version 1.9.3 (Apple Git-50)
	{% endhighlight %}	
This version is **NOT** patched. 
<br><br>
Furthermore if you type, 
	{% highlight text %}
	which git
	{% endhighlight %}		
and it returns
	{% highlight text %}
	/usr/local/bin/git
	{% endhighlight %}		
Then you are going to want to modify your PATH to make git look for the official distro (which we will install in just a sec) to just /usr/local/bin.<br>

## Let's Fix it and switch Git Clients

Install [Homebrew](http://brew.sh) if you haven't already. It is easy just copy and paste this in the terminal window. 
	{% highlight text %}
	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	{% endhighlight %}		
Assuming you have homebrew installed, type the following: 
	{% highlight text %}
	brew install git
	{% endhighlight %}		
Once it is installed, then type the following two lines, which will set our path to the local git distro instead of the Apple one.  
	{% highlight text %}
	export PATH=/usr/local/bin:$PATH
	git --version
	{% endhighlight %}		
and you will see:
	{% highlight text %}
	git version 2.2.1
	{% endhighlight %}		
That is it! You are now updated to the official distro of Git on your Mac. To update it in the future all you will need to do is run the following line:
	{% highlight text %}
	brew upgrade git
	{% endhighlight %}		
Until next time, Michael signing off.


