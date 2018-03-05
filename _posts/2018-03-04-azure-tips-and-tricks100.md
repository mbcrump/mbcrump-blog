---
layout: post
title: "Azure Tips and Tricks Part 100 - Creating an Email Subscription with Azure Functions - Sending Emails"
excerpt: "Learn how to generate a weekly digest email for a blog using Azure Functions, SendGrid and Azure Storage"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**We made it to 100!** This series has been dedicated to YOU! Thank you for reading these and providing words of encouragement along the way. I couldn't have done it without you. If you want to subscribe to my Weekly Digest then you can do so [here](https://www.michaelcrump.net/about/emailsub.html).
{: .notice--info}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of 100 Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Where are we?

**Full Source Code** The source code for the app can be found on [GitHub](https://github.com/mbcrump/EmailSubscription)
{: .notice--info}

This blog post is part of a series on how to generate a weekly digest email for a blog using Azure Functions, SendGrid and Azure Storage. 

* [Part 1 - What we're going to build and how to build it](http://www.michaelcrump.net/azure-tips-and-tricks97/)
* [Part 2 - Storing Emails using Azure Table Storage](http://www.michaelcrump.net/azure-tips-and-tricks98/)
* [Part 3 - Writing the Frontend with HTML5 and jQuery](http://www.michaelcrump.net/azure-tips-and-tricks99/)
* [Part 4 - Sending Emails with Sendgrid and Azure Functions](http://www.michaelcrump.net/azure-tips-and-tricks100/)

We're trying to build a Email Subscription similar to the following. If you want to catch up, then read the previous posts. 

<img style="border:3px solid #021a40" src="/files/emailsub1.png">

## Generating and Sending Emails

In our last post, we left off by creating a frontend that used HTML5, jQuery and some light CSS work. When the user filled out the form and clicked **Submit**, then it would check to ensure the email is valid and then use an AJAX call to POST the data to our Azure Function that we wrote in part 2. Today, we'll wrap things up by using SendGrid, C# and Azure Functions to send emails every Sunday at 9:30AM. 

## Use the Azure Functions Template inside of Visual Studio

Return to the project we created earlier and right-click the project and select **Add Item** and select **Azure Functions**. Now give it a name such as **SendEmail** and select **Timer Trigger** and provide the following schedule **0 30 9 * * SUN**.

<img style="border:3px solid #021a40" src="/files/emailsub5.png">

We'll begin by declaring the feedurl and looping through the feed to collect the last 7 days worth of blog posts and append them to a string. Here we are using SyndicationClient to make easier work of everything. We could also use StringBuilder but for now this will do. 

```csharp
string feedurl = "https://www.michaelcrump.net/feed.xml";
string last7days = "";

XmlReader reader = XmlReader.Create(feedurl);
SyndicationFeed feed = SyndicationFeed.Load(reader);
reader.Close();

last7days = last7days + "<b>New updates in the last 7 days:</b><br><br>";
foreach (SyndicationItem item in feed.Items)
{
    if ((DateTime.Now - item.PublishDate).TotalDays < 7)
    {
        last7days = last7days + "<a href=\"" + item.Links[0].Uri + "\">" + item.Title.Text + "</a><br>";
    }       
}
```

We'll now grab a list of our **EmailSubscribers** that is in our Azure Storage Table. 

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["TableStorageConnString"]);
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("MCBlogSubscribers");
table.CreateIfNotExists();
```

We'll need to add this helper method outside of the **Run** method we are currently in. It will search for the **Partition Key** that matches what we sent in our POST request in post #2. 

```csharp
public static List<string> GetAllEmailAddresses(CloudTable table)
{
    var retList = new List<string>();

    TableQuery<EmailEntity> query = new TableQuery<EmailEntity>()
            .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "SendEmailToReaders"));

    foreach (EmailEntity emailname in table.ExecuteQuery(query))
    {
        retList.Add(emailname.EmailAddress);
    }

    return retList;
}
```

Now we need to send our emails. This is where it gets slightly tricky as we need to use the **X-SMTPAPI** header to hide the email address of all our users. Search **NuGet** and add **Sendgrid.SmtpApi** to your references. We'll need to get our SendGrid Username and Password and pass them in the credentials. 

```csharp
var header = new Header();

SmtpClient client = new SmtpClient();
client.Port = 587;
client.Host = "smtp.sendgrid.net";
client.Timeout = 10000;
client.DeliveryMethod = SmtpDeliveryMethod.Network;
client.UseDefaultCredentials = false;
client.Credentials = new System.Net.NetworkCredential(ConfigurationManager.AppSettings["SendGridUserName"], ConfigurationManager.AppSettings["SendGridSecret"]);
```

Now we need to form our email message. We'll pull the list of email addresses from our Azure Storage Table and force the HTML view to ensure our links are clickable and tell those that don't have HTML enabled, to enable it. :) 

Finally, we'll send the email asynchronously and dispose of our client. 

```csharp
MailMessage mail = new MailMessage();
List<string> recipientlist = GetAllEmailAddresses(table);
header.SetTo(recipientlist);
mail.From = new MailAddress("michael@michaelcrump.net", "Azure Tips and Tricks");
mail.To.Add("no-reply@michaelcrump.net");
mail.Subject = "Weekly Digest for MichaelCrump.net Blog";
mail.BodyEncoding = Encoding.UTF8;
mail.SubjectEncoding = Encoding.UTF8;

AlternateView htmlView = AlternateView.CreateAlternateViewFromString(last7days);
htmlView.ContentType = new System.Net.Mime.ContentType("text/html");
mail.AlternateViews.Add(htmlView);
mail.Body = "Please enable HTML in order to view the message";

mail.Headers.Add("X-SMTPAPI", header.JsonString());

await client.SendMailAsync(mail);

mail.Dispose();
```

Before we publish the updates to our Azure Function, we'll need to ensure that users can unsubscribe easily. I was originally going to handle this myself, but it is super simple with SendGrid. 

Log into your [SendGrid](https://app.sendgrid.com/) account and go to **Settings** and then **Tracking** and you'll see **Subscription Tracking**. If you turn this on, then it will add the unsubscribe link for you and manage those users. NEAT!

<img style="border:3px solid #021a40" src="/files/emailsubtracking.png">

Now is a great time to go ahead and publish our Azure Function. Simply right click the project name and select Publish, then Publish again as shown below.

<img style="border:3px solid #021a40" src="/files/emailsub8.png">

Once it deploys, if you click on the **SendEmail** function, then you can run it (note you can also run it inside of Visual Studio).

It should say that it compeleted successfully, and now go check your email and it should be working. 

<img style="border:3px solid #021a40" src="/files/emailcompletedsuccessfully.png">

And we're done! If something isn't working then check the source code for the app on [GitHub](https://github.com/mbcrump/EmailSubscription) and if you have any questions then ping me on [twitter](http://twitter.com/mbcrump). You should follow me btw, I might have another tip and trick to share! 

If you want to subscribe to my Weekly Digest and use the form, then you can do so [here](https://www.michaelcrump.net/about/emailsub.html).

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 