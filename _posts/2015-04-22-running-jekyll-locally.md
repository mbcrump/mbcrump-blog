---
layout: post
title: "Running your Jekyll blog on a Local Server"
excerpt: "A quick way to run Jekyll locally."
tags: [jekyll, blog, ruby]
comments: true
---

### Introduction

I recently hit a stumbling block when trying to serve my Jekyll blog locally. After I ran the command 'bundle exec jekyll serve', I noticed that my local server would spin up, but the links would all point back to http://michaelcrump.net/whatever-blog-post. When they should be pointing to http://127.0.0.1:4000/whatever-blog-post.
<br><br>
The fix is quite simple:<br>
<br>
Open your _config.yml file and add the following line (replace my domain name with yours): 
	{% highlight text %}
	baseurl:          http://michaelcrump.net
	{% endhighlight %}
Next, at your terminal prompt enter the following command to serve your site locally:
	{% highlight text %}
	bundle exec jekyll serve --baseurl ''
	{% endhighlight %}	
<br>
This simply overwrites the baseurl value with no value. 
Now simply navigate out to [http://127.0.0.1:4000/](http://127.0.0.1:4000/) and your links should be pointing to the local version instead of your github page or custom domain.

> Note: There are other ways that you can maintain two .yml files (one for development and one for production) located [here](http://www.jaredwolff.com/blog/jekyll-local-preview/). 

I hoped this helped!


