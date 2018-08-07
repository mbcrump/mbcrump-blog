---
layout: post
title: "Azure Tips and Tricks Part 147 - Run TSQL on an Azure SQL database with Azure Functions"
excerpt: "Learn how to run TSQL on an Azure SQL database with Azure Functions"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Run TSQL on an Azure SQL database with Azure Functions

I've recently been adding Azure SQL tips such as [Easily reset the Administrator password for an Azure SQL database](http://www.michaelcrump.net/azure-tips-and-tricks145/) and [Rename an Azure SQL database](http://www.michaelcrump.net/azure-tips-and-tricks146/). and you all seem to like them. So I'm back with another SQL post that addresses another common scenario that folks ask "How do I run TSQL on an Azure SQL database with Azure Functions"?

### SQL Database

Before we begin you'll need to grab the connection string from the database you created earlier. Simply select **SQL Databases** and select your database on the SQL databases page.

Click **Show database connection strings** and copy the string to your clipboard.

<img style="border:3px solid #021a40" src="/files/azconstring1.png">

Go ahead and replace {your_username} and {your_password} placeholders with real values and save it somewhere easily accessible.

### Azure Functions

Create a new Azure Function and select Timer Trigger. You typically want to store this secret in **Platform features > Application settings** in the **Connection strings** placeholder. So go ahead and do that as shown below:

<img style="border:3px solid #021a40" src="/files/azconstring2.png">

Now use the following code

```csharp
#r "System.Configuration"
#r "System.Data"

using System.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;

public static async Task Run(TimerInfo myTimer, TraceWriter log)
{
    var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
    using (SqlConnection conn = new SqlConnection(str))
    {
        conn.Open();
        var text = "UPDATE MichaelTestDB.User " + 
                "SET [Item] = 5  WHERE DateAdded < GetDate();";

        using (SqlCommand cmd = new SqlCommand(text, conn))
        {
            var rows = await cmd.ExecuteNonQueryAsync();
        }
    }
}

```

Nice! Now you can run any TSQL command and output the results to whatever you want such as SendGrid for email, Twilio for SMS, etc. Unlimited possibilities!


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 