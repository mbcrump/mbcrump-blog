---
layout: post
title: "Azure Tips and Tricks Part 73 - Send Emails through Azure with C# and SendGrid"
excerpt: "Learn how to send emails through Azure with C# and SendGrid"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

**Want to contribute?** I'm currently looking for folks who want to contribute to Azure Tips and Tricks. If you are interested, then read [more here](https://github.com/mbcrump/mbcrump-blog/blob/master/contributing/index.md).
{: .notice--info}

**Upcoming Schedule** Azure Tips and Tricks resumes with our normal posting schedule starting next Sunday (1/7).
{: .notice--danger}

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Send Emails through Azure with C# and SendGrid

In this post, I'll walk through the process that I completed to create an account with SendGrid and send an email with C#.

Go to the **Azure Portal** and search services for **SendGrid** and create an account as shown below. You'll notice that I used the **Free** account as it is good enough for what I was trying to accomplish. 

<img style="border:3px solid #021a40" src="/files/sendgrid1.png">

Go to your SendGrid account once provisioned and click on **Manage** and it will bring you to [https://app.sendgrid.com/](https://app.sendgrid.com/) as shown below. 

<img style="border:3px solid #021a40" src="/files/sendgrid2.png">

From the SendGrid portal, you are going to want to grab your API key. You can find it under **Settings**, then **API Keys**

<img style="border:3px solid #021a40" src="/files/sendgrid3.png">

Give your API Key a name and then give it **Full Access** and click **Create and View**. 

<img style="border:3px solid #021a40" src="/files/sendgrid4.png">

**Remember this!** Copy this key somewhere safe as we'll be using it again shortly!
{: .notice--primary}

Now that you have your API Key, open Visual Studio and create a new Console Application. (Keep in mind this could be an Azure Function for example). You'll need to add in the **Sendgrid** NuGet package (which you can do from Manage NuGet packages). 

<img style="border:3px solid #021a40" src="/files/sendgrid5.png">

Insall the NuGet package and copy and paste the following C# code into your Console application, simply replacing your API key.

```csharp
    class Program
    {
        static void Main(string[] args)
        {
            Execute().Wait();

        }
        static async Task Execute()
        {
            var client = new SendGridClient("ENTER-YOUR-API-KEY-HERE");
            var msg = new SendGridMessage();

            msg.SetFrom(new EmailAddress("a@gmail.com", "Azure Tips and Tricks"));

            var recipients = new List<EmailAddress>
                {
                    new EmailAddress("a@gmail.com"),
                    new EmailAddress("b@gmail.com"),
                    new EmailAddress("c@gmail.com")
                };
            msg.AddTos(recipients);

            msg.SetSubject("Mail from Azure and SendGrid");

            msg.AddContent(MimeType.Text, "This is just a simple test message!");
            msg.AddContent(MimeType.Html, "<p>This is just a simple test message!</p>");
            var response = await client.SendEmailAsync(msg);

        }
    }
```

Run the application and check whatever email that you sent it to!

<img style="border:3px solid #021a40" src="/files/sendgrid6.png">

The source code can be found [here](https://github.com/mbcrump/sendgrid). 

## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 