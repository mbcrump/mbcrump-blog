---
layout: post
title: "Azure Tips and Tricks Part 99 - Creating an Email Subscription with Azure Functions - Writing the Frontend"
excerpt: "Learn how to generate a weekly digest email for a blog using Azure Functions, SendGrid and Azure Storage"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Azure Developer Guide Book 2nd Edition available now!** This free eBook is available now at [aka.ms/azuredevebook](https://aka.ms/azuredevebook).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Where are we?

This blog post is part of a series on how to generate a weekly digest email for a blog using Azure Functions, SendGrid and Azure Storage. 

* [Part 1 - What we're going to build and how to build it](http://www.michaelcrump.net/azure-tips-and-tricks97/)
* [Part 2 - Storing Emails using Azure Table Storage](http://www.michaelcrump.net/azure-tips-and-tricks98/)
* [This post - Writing the Frontend with HTML5 and jQuery](http://www.michaelcrump.net/azure-tips-and-tricks99/)
* [Coming Soon - Sending Emails with Sendgrid and Azure Functions](http://www.michaelcrump.net/azure-tips-and-tricks100/)

We're trying to build a Email Subscription similar to the following. If you want to catch up, then read the previous posts. 

<img style="border:3px solid #021a40" src="/files/emailsub1.png">

## Writing the frontend

In our last post, we left off by creating an Azure Function that had the ability to accept a POST request and store data using Azure Table Storage for our email address. While this works great in something like Postman, we need to create a way to allow a user to interact with it.

Now is a great time to go ahead and publish our Azure Function. Simply right click the project name and select **Publish**, then **Publish** again as shown below. 

<img style="border:3px solid #021a40" src="/files/emailsub8.png">

Once it deploys, if you click on the **StoreEmail** function, then you'll see a **Get Function URL** as shown below. 

<img style="border:3px solid #021a40" src="/files/emailsub9.png">

If you click it, then copy and paste the Function url as you'll use that later. 

<img style="border:3px solid #021a40" src="/files/emailsub10.png">

## Dealing with CORS

While we're in the portal, click on your Azure Function and under **Platform Features**, you'll see **API** and then **CORS**. 

Cross-Origin Resource Sharing (CORS) allows JavaScript code running in a browser on an external host to interact with your backend. 
{: .notice--info} 

Since we'll be moving this to a web host shorly, you'll want to specify your domain name. Here is mine:

<img style="border:3px solid #021a40" src="/files/emailsub11.png">

## Finally, the frontend. 

Create a new .HTML page anywhere and begin by adding the following code:

```html

 <h1>Subscribe to the Weekly Digest</h1>
 Subscribe to MichaelCrump.net
 <form id="target">
 <div id="contactForm">
     Your Email: <input type="text" name="fromEmail" /><br />
     <input type="submit" value="Send!" />
 </div>
</form>

<div id="contactFormStatus">
    </div>
```

This gives us a **form** alongwith an **input** type for our email address and a **submit** button. We also have a **div** tag to show status. 

Now we'll use jQuery and a Ajax call to POST the email address to our Azure Function url that we copied earlier. That **div** tag that we had that showed status will not be used to output success or failure. 

```html
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
 <script type="text/javascript">
      var url = "https://functionsendemails.azurewebsites.net/api/StoreEmail?code=hKngrr6sq35GJ8cb6al4K6oP0cRphKNDMXpLrCtoNCJzM0ZDwJNkJQ==";
     $("form").on('submit', function (event) {
         event.preventDefault();
  
         var data = $(this).serialize();

         $("#contactFormStatus").hide();
         $("#target :input").prop("disabled", true);

         $.ajax({
             type: "POST",
             url: url,
             data: data,
             dataType: "text",
             headers: {'Content-Type': 'application/x-www-form-urlencoded'},
             success: function (respData) {
                 $("#contactFormStatus").html("<div style='padding: 5em 1em; text-align: center; color: #001088'>" + respData + "</div>");
             },
             error: function (jqXHR) {
                 $("#contactFormStatus").html("<div style='padding: 1em; text-align: center; color: #d20808'>An error occurred: " + jqXHR.responseText + "</div>");
                 $("#contactFormStatus").show();
                 $("#target :input").prop("disabled", true);
             }
         });
     });
 </script>
```

If you try to run the code on your server then you'll see it works as designed. You can also use something like Azure Storage Explorer to see the data in the table. 

<img style="border:3px solid #021a40" src="/files/emailsub11.gif">

Come back next week and we'll wire up the Email functionality with Sendgrid. Happy Coding!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 