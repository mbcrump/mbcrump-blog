---
layout: post
title: "Writing an Azure Function to add an ICS file to your calendar"
excerpt: "Learn how that I wrote an Azure Function to help promote the Azure Function webinar"
tags: [azure, windows, cli, csharp]
share: true
comments: true
---

## Intro

A couple of weeks ago, I used an online tool to create an ICS file for an upcoming Azure Functions Webinar. After I tweeted it, I saw this recommendation from a friend of mine named Carl Schweitzer (@carlschweitzer)  : 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">You need to have an Azure Function serve up your ICS file. That would be awesome!</p>&mdash; Carl Schweitzer (@carlschweitzer) <a href="https://twitter.com/carlschweitzer/status/870833270912692224">June 3, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Fair enough! It sounded like a great idea, so this is my journey following his tweet. 

## Setting it all up! 

Since I used an online tool to create the ICS file, I knew that I was going to have to generate an ICS file from my site and that it would be used all over the world. It would also need to work with a variety of email clients, including online ones. I also wanted folks to just go to a website and it would generate and send down the ICS file. This would also allow  me to easily modify it for future webinars. 

With that in mind, I began by taking a look at a third party library called [iCal.NET](https://github.com/rianjs/ical.net). It looks like this handles all the various time zones and client. Next, I opened the Azure Portal and creating a new Azure Function application securing the name that folks would go to : 
 
![image](/files/azure-new-app1.png)

Next, I chose a language and happily picked C# (*Amazon AWS Lambdas only supports C# via .NET Core*) and used a HttpTrigger template. How cool is it to have templates like this?!?

![image](/files/azure-quickstart-templates.png)

By default, the code in the template is looking for a name parameter and a POST command. Since, I didn't want to respond to a POST, but rather just a GET, I used this as my start but deleted the name parameter section. 

Armed with just the online editor, I started writing code. I could have downloaded [Visual Studio 2017 Preview 3](https://www.visualstudio.com/vs/preview/) and the [Azure Function tooling](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) for a richer debugging experience, but it was getting late and I wanted to crank this out with just a browser and my C# skills. 

I needed to pull in a third party library, so I noticed that you could view "Files" inside the portal and that it supports NuGet. I simply created a `project.json` and added the following NuGet package reference to iCal.NET and Newtonsoft.Json : 

	{
	  "frameworks": {
	    "net46": {
	      "dependencies": {
	        "Ical.Net": "2.2.19",
	        "Newtonsoft.Json": "9.0.1"
	      }
	    }
	   }
	}

When I switched back to my function, I noticed my project started pulling down the references and restarted my function. 

## Writing the code

I finally landed on the following code after reading the iCal.NET docs and learning more about HttpRequestMessage : 

	using System.Net;
	using Ical.Net;
	using Ical.Net.DataTypes;
	using Ical.Net.Serialization;
	using Ical.Net.Serialization.iCalendar.Serializers;
	using Newtonsoft.Json.Linq;
	using System;
	using System.Collections.Generic;
	using System.Net.Http;
	using System.Net.Http.Headers;
	using System.Threading.Tasks;
	using System.Text;
	
	public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
	{
	    var calendar = new Calendar();
	    calendar.AddProperty("X-WR-CALNAME", "Azure Functions Webinar"); // sets the calendar title
	    calendar.AddProperty("X-ORIGINAL-URL", "http://aka.ms/AzureFunctionsLive");
	    calendar.AddProperty("METHOD", "PUBLISH");
	  
	    var icalevent = new Event()
	        {
	            DtStart = new CalDateTime(new DateTime(2017, 07, 06, 18, 0, 0, DateTimeKind.Utc)),
	            DtEnd = new CalDateTime(new DateTime(2017, 07, 06, 19, 0, 0, DateTimeKind.Utc)),
	            Created = new CalDateTime(DateTime.Now),
	            Location = "http://aka.ms/AzureFunctionsLive",
	            Summary = "Azure Function Webinar",
	            Url = new Uri("http://aka.ms/AzureFunctionsLive")
	        };
	
	    string description = "Join the Azure Functions team as we cover some cool tips and tricks, review what's coming next and take your questions!";
	
	    icalevent.AddProperty("X-ALT-DESC;FMTTYPE=text/html", description); // creates an HTML description
	    calendar.Events.Add(icalevent);
	
	    var serializer = new CalendarSerializer(new SerializationContext());
	
	    var serializedCalendar = serializer.SerializeToString(calendar);
	    var bytesCalendar = Encoding.UTF8.GetBytes(serializedCalendar);
	    var result = new HttpResponseMessage(HttpStatusCode.OK)
	    {
	        Content = new ByteArrayContent(bytesCalendar)
	    };
	
	    result.Content.Headers.ContentDisposition =
	        new System.Net.Http.Headers.ContentDispositionHeaderValue("attachment")
	    {
	        FileName = "webinarinvite.ics"
	    };
	
	    result.Content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
	
	    return result;
	}

The code is pretty self-explanatory if you've used iCal.NET before, but basically I create the file and ensure when someone visits the site that it sends down an ICS file named `webinarinvite.ics`. 

During the process of working with the function, I hit the "Save" button and it would let me know if it compiled successfully or not. It finally compiled successfully as shown below : 

	2017-06-06T23:19:02  Welcome, you are now connected to log-streaming service.
	2017-06-06T23:20:02  No new trace in the past 1 min(s).
	2017-06-06T23:23:04.794 Function started (Id=xxx-1d71-4f1f-8fbd-6d1b4dcc96f0)
	2017-06-06T23:23:05.921 Function completed (Success, Id=xxx-1d71-4f1f-8fbd-6d1b4dcc96f0, Duration=1137ms)

Very cool! Now to test the function, it was as simple as selecting **GET** from the dropbox on the Test Tab and hitting the **Run** button. 

![image](/files/testazurefunctions.png)

Now that my function was working properly, I grabbed the URL to my app and pasted it into the browser. The URL was easy to find as shown below:  

![image](/files/azurefunctionurl.png)

Success! It downloaded the .ICS file and after opening it, the following entry appeared in my calendar : 

![image](/files/azurewebinar.png)

I've recently checked the traffic using the "Monitor" section and noticed it has already received 393 downloads! 

![image](/files/azurestatsfunction.png)

Whenever I need to update this in the future, all it will require is changing two lines. No additional servers, redeployment, etc. is needed as it will auto compile. 

Not only did it solve our business needs, but I think have the webinar available for later viewing even saved a marriage! 

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">I am committed to making sure no marriage is at risk by attending our webinar. 😀</p>&mdash; Michael Crump 🤓 (@mbcrump) <a href="https://twitter.com/mbcrump/status/872834934938808320">June 8, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Btw, you can try it now at [http://aka.ms/AzureFunctionsLive](http://aka.ms/AzureFunctionsLive) and be sure to follow [@AzureFunctions](https://twitter.com/AzureFunctions) on Twitter! 

## Wrap-up

This really shows the power of [Azure Functions](https://azure.microsoft.com/en-us/services/functions/) and I'm very excited about Serverless! As always, thanks for reading and smash one of those share buttons to give this post some love if you found it helpful. Also, feel free to leave a comment below or follow me on [twitter](http://twitter.com/mbcrump) for daily links and tips. 