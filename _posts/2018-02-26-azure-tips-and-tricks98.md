---
layout: post
title: "Azure Tips and Tricks Part 98 - Creating an Email Subscription with Azure Functions - Storing Emails"
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
* [This Post - Part 2 - Storing Emails using Azure Table Storage](http://www.michaelcrump.net/azure-tips-and-tricks98/)
* [Coming soon - Writing the Frontend with HTML5 and jQuery](http://www.michaelcrump.net/azure-tips-and-tricks99/)
* [Coming soon - Sending Emails with Sendgrid and Azure Functions](http://www.michaelcrump.net/azure-tips-and-tricks100/)

We're trying to build a Email Subscription similar to the following. If you want to catch up, then read the previous post. 

<img style="border:3px solid #021a40" src="/files/emailsub1.png">

## Continuing where we left off

We recently created a Visual Studio project that used the Azure Functions template. We used NuGet to pull in references to the following packages that we'll be working with shortly:

* WindowsAzure.Storage `To work with Azure Table Storage.`
* Microsoft.WindowsAzure.ConfigurationManager `To hide our API keys`
* Sendgrid `To send our emails`
* System.ServiceModel.Syndication `To work with RSS feeds - use prerelease packages to find it`

Right click the project and select **Add Item** and select **Azure Functions**. Now give it a name such as **StoreEmail** and select **Http Trigger** along with the defaults as shown below.

<img style="border:3px solid #021a40" src="/files/emailsub6.png">

We only need this to be a **post** request, so modify the **Run** method's signature to match the following :

`[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)]`

Since we'll be working with Azure Table Storage, we need to setup a class that has two fields: 

* EmailAddress - to store the email that the user typed in
* Unsubscribe - to keep track if they want to unsubscribe from the newsletter (by default it will be set to no, and they'll have a chance to opt-out in the email)

```csharp
class Email : TableEntity
{

    public string EmailAddress { get; set; }
    public bool Unsubscribe { get; set; }

    public Email(string email, bool unsub)
    {
        EmailAddress = email;
        Unsubscribe = unsub;
        PartitionKey = "SendEmailToReaders";
        RowKey = Guid.NewGuid().ToString();
    }

    public Email()
    {

    }
}

```

I also have a helper class that we'll use to store the data, so add the following which will allow us to pass a table object and a new email instance: 

```csharp
static void CreateMessage(CloudTable table, Email newemail)
{
    TableOperation insert = TableOperation.Insert(newemail);

    table.Execute(insert);
}
```

Finally, we'll need add the code for the **Run** method: 

```csharp
public static async Task<HttpResponseMessage> Run([HttpTrigger(AuthorizationLevel.Function, "post", Route = null)]HttpRequestMessage req, TraceWriter log)
{

//(Block #1)
    var postData = await req.Content.ReadAsFormDataAsync();  
    var missingFields = new List<string>(); 
    if (postData["fromEmail"] == null)
    {
        missingFields.Add("fromEmail");
    }

    if (missingFields.Any())
    {
        var missingFieldsSummary = String.Join(", ", missingFields);
        return req.CreateResponse(HttpStatusCode.BadRequest, $"Missing field(s): {missingFieldsSummary}");
    }
//(End Block #1)

//(Block #2)
    try
    {

        //CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["TableStorageConnString"]); to be used later on
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("AzureStorageAPIKey");
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
        CloudTable table = tableClient.GetTableReference("MCBlogSubscribers");
        table.CreateIfNotExists();

        CreateMessage(table, new Email(postData["fromEmail"], false));
        return req.CreateResponse(HttpStatusCode.OK, "Thanks! I've successfully recieved your request. ");
    }
    catch (Exception ex)
    {
        return req.CreateResponse(HttpStatusCode.InternalServerError, new
        {
            status = false,
            message = $"There are problems storing your email address: {ex.GetType()}"
        });
    }
//(End Block #2)
}
```
**Keep in mind, you'll need to pull in your using references!**{: .btn .btn--success} 

Block #1 is all about pulling in the POST data and checking to see if an email address is being sent. If it is, then it will send a summary of what fields are missing. 

Block #2 tries to save the input via the Azure Table Storage account that we created and if it saves successfully, then returns to the client everything went fine. Otherwise, output to the client what the problem was. Keep in mind, that we'll be using **ConfigurationManager** later, once we deploy the site. 

Hit the Run button in Visual Studio and you'll see the following: 

<img style="border:3px solid #021a40" src="/files/emailsub7.png">

Make note of the localhost where it is running and use something like **POSTMAN** to test your POST call. Below, I've configured Postman to my localhost URL and supplied an email address. You'll see at first, I don't supply anything and it returns an error. I then try it again and it returns that it was successful. 

<img style="border:3px solid #021a40" src="/files/emailsub7.gif">

Come back tomorrow where we'll write a frontend that uses HTML and jQuery to send the POST data. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 