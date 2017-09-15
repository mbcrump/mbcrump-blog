---
layout: post
title: Fixing Migration Problems from Xcode 6 to Xcode 7
excerpt: A quick solution to fix a common problem when migrating existing Swift apps to Xcode 7.
tags: blog
comments: true
---

## The Issue

After running the Xcode 7 migration wizard for my [Tasks Application](https://github.com/mbcrump/TasksForSwiftWithPersistingData) written in Xcode 6, I noticed the following error: 

{% highlight text %}
directory not found for option '-F/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/SDKs/iPhoneSimulator9.0.sdk/Developer/Library/Frameworks'
{% endhighlight %}

You can see the error in Xcode 7 below. It provides no additional information on how to resolve it. 

![image](/files/directorynotfounderror.jpg)

After much digging, I found this is actually related to my test target of my app. 

![image](/files/taskapptest.jpg)

## The Fix

If you select your project, and look under 'Targets', you should see two targets. One is your app and the other one is your test. Under 'Search Paths' (in my test target), I found it was including two items under 'Framework Search Paths':

{% highlight text %}
$(SDKROOT)/Developer/Library/Frameworks
$(inherited)
{% endhighlight %}

$(SDKROOT)/Developer/Library/Frameworks $(inherited)

![image](/files/searchpathentries.jpg)

Deleting those entries in my older project then removed the warning. I did not have to make any changes to the other target. 

## Like this Post?

As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below. 

