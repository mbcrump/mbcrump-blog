---
layout: post
title: "Azure Tips and Tricks Part 167 - Migrating Data from Cosmos DB to Local JSON files"
excerpt: "Learn how to use migrating data from cosmos db to local json files"
tags: [azure, database, json, cosmosdb]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}


## Migrating Data from Cosmos DB to Local JSON files

## Using the Data Migration Tool with Cosmos DB

One tasks that seems to come up over and over is migrating data from one database/format into another. I recently used Cosmos DB as my database to store every tweet that came out of Ignite. Once I had the data and wouldn't be using Cosmos DB any more for that exercise, I needed to dump the data out to a local file to preserve the data and save money. Here is how I did it. 

## The Tools

Download and install the [Azure DocumentDB Data Migration Tool](https://www.microsoft.com/en-us/download/confirmation.aspx?id=46436)

# Get to Work

Ensure you have a Cosmos DB database and collection created that you wish to migrate out. 

Go to **Keys** (inside your Cosmos DB blade in the portal) to copy the **Primary Connection String**

<img style="border:3px solid #021a40" src="/files/migrationcosmos2.png">

You'll need to append the Database name to the end of the string. For example `Database=cosmosdb-ignite` will be appended to the **Key** copied earlier `AccountEndpoint=https://mbcrump.documents.azure.com:443/;AccountKey=VxDEcJblah==;Database=cosmosdb-ignite`. Save this for later. 

Open the **Data Migration Tool** and under **Source Information**, select **DocumentDB** as shown below. 

You'll need to add the **ConnectionString** (that we just created) along with the **Collection** and in my case it is `items`. We'll take the defaults on the rest and press **Verify** and if successful, then press **Next**.

<img style="border:3px solid #021a40" src="/files/migratingdatafromcosmosdb-1.png">

In my case, I'll export to a local JSON file and select **Prettify JSON** and press **Next**.

<img style="border:3px solid #021a40" src="/files/migratingdatafromcosmosdb-2.png">

On the next screen, you'll see a **View Command** to see the command that will be used to migrate your data. This is helpful to just learn the syntax. 

<img style="border:3px solid #021a40" src="/files/migratingdatafromcosmosdb-3.png">

<img style="border:3px solid #021a40" src="/files/migratingdatafromcosmosdb-4.png">

You'll finally see the Import has completed with over 100K items transferred in a little under 2 minutes. 

<img style="border:3px solid #021a40" src="/files/migratingdatafromcosmosdb-5.png">

We now have our local JSON file and can use it however we want! Awesome!

**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
