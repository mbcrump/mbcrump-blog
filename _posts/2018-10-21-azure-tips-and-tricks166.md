---
layout: post
title: "Azure Tips and Tricks Part 166 -  Data Storage Options with Azure Storage and Cosmos DB"
excerpt: "Learn about different storage options in Azure"
tags: [azure, cosmosdb, portal, cloud, tablestorage]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## Azure Table Storage and Azure Cosmos DB

Before you dive into this article, keep in mind that this is not a comparison and use what you feel is right for your scenario. 

## Azure Table Storage in a nutshell

[Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) offers a NoSQL key-value store for semi-structured data. 
Unlike a traditional relational database, each entity (such as a row - in relational database terminology) can have a different structure, allowing your application to evolve without downtime to migrate between schemas.

## Azure Cosmos DB in a nutshell

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a multimodal database service designed for global use in mission-critical systems. Not only does it expose a Table API, it also has a SQL API, Apache Cassandra, MongoDB, Gremlin and Azure Table Storage. These allow you to easily swap out existing dbs with a Cosmos DB implementation. 

## Performance

Azure Table Storage has no upper bound on latency. Cosmos DB defines latency of single-digit milliseconds for reads and writes along with operations at sub-15 milliseconds at the 99th percentile worldwide. (That was a mouthful) Throughput is limited on Table Storage to 20,000 operations per second. On Cosmos DB, there is no upper limit on throughput, and more than 10 million operations per second are supported. Unlike Table Storage, Cosmos DB automatically indexes on all properties, and queries can take advantage of this to improve performance.

## Global Distribution

Azure Table Storage supports a single region with an optional read-only secondary region for availability. Cosmos DB supports distribution from 1 to more than 30 regions with automatic failovers worldwide. You can easily manage this from the Azure portal and define the failover behavior. Five defined consistency levels allow you to select the right balance between availability, latency, throughput, and consistency.

## Billing

Azure Table Storage uses storage volume to determine billing. It is priced per GB and the rates vary depending on the redundancy level selected. Pricing is tiered to get progressively cheaper per GB the more storage you use. Operations incur a charge measured per 10,000 transactions. All operation types are treated the same.

For Cosmos DB, throughput is measured in request units (RU)is also billed. The database is provisioned with a level of throughput in increments of 100 RU per second. These are billed hourly and you can elastically scale to meet changes in workload. This is in addition to a storage rate at a higher price per GB. Therefore, if your requirements are more modest and you don't have the need for the additional performance and redundancy options, Azure Table Storage could be an option. But this may seem like something that's very difficult to calculate, but there is an online tool that makes it easy for you to estimate costs.
 
<img style="border:3px solid #021a40" src="/files/azure-cosmos-planner.png">

Calculator for estimating request units and data storage can be found at : https://www.documentdb.com/capacityplanner.

## Consistent API

Both Azure Table Storage and Azure Cosmos DB support the same [Table API](https://docs.microsoft.com/en-us/azure/cosmos-db/table-introduction). SDKs are available for common programming environments along with a generic REST API. Because Cosmos DB exposes a superset of functionality, there are some overloaded API methods to specify additional options. The common API makes it easier to migrate a solution from Azure Table Storage to Cosmos DB as it grows. It also makes learning the API easier. You can target Azure Table Storage, Azure Cosmos DB, or the Azure storage emulator running location by simply replacing the connection string.

## A Code Sample

Sometimes I like to just look at the code vs. writing a full app and here is an example of accessing the Table API mentioned above. 

In code, I'd create an instance of **CloudStorageAccount** passing your connection string. Then, from this object, you can call **CreateCloudTableClient()** to return the **CloudTableClient** object that can work with the Table Storage or Cosmos DB instance. To create a new table requires just two further lines of code: first, **GetTableReference(tablename)**; then, call **CreateIfNotExists** on the returned **CloudTable**.

To create entities to store in your table, they have to be classes derived from **TableEntity**. This base class handles the serialization of the entity into a format that can be stored in the database. It also has standard properties for **PartitionKey** and **RowKey** that provide a unique identity for the item.

An individual operation on the table is performed with either a **TableOperation** or a **TableBatchOperation** for multiple items. You create a new operation, set up the actions to perform, and then call Execute on the **CloudTable** passing the operation object. 

```
EmployeeEntity employee1 = new EmployeeEntity("Case", "Justin");
employee1.Email = "justin@contoso.com";
employee1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the employee entity.
TableOperation insertOperation = TableOperation.Insert(employee1);

// Execute the insert operation.
table.Execute(insertOperation);
```

In addition to **Insert**, **Retrieve**, **Replace**, and **Delete** operations, there is an **InsertOrReplace** operation that will overwrite an entity matching the partition and row key.

## Migration

If you have existing data in Azure Table Storage, you can migrate it to Cosmos DB using the [Data Migration tool](https://docs.microsoft.com/en-us/azure/cosmos-db/import-data) or [AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy). Cosmos also supports import from other databases such as MongoDB. You may choose to start development with Table Storage and then migrate to Cosmos as your requirements evolve. Because the API is the same there is no impact to the code you write.

## Wrapping up

So far we've covered a lot of information, this handy table below should help make sense of it all.

|            | Azure Table Storage | Azure Cosmos DB |
| ---------- | ------------------- | --------------- |
| Throughput | Up to 20K operations per second | No upper limit, supports >10M operations per second |
| Redundancy | One optional secondary read-only region | Multiple configurable worldwide regions |
| Latency | No upper bounds | Single-digit milliseconds |
| Consistency | Strong and Eventual consistency models | Five defined consistency models |
| Query | Optimized for query on primary key | Improved query performance because all fields are indexed |
| Failover | Can't initiate failover | Automatic and manual failovers |
| Billing | Storage-based | Throughput-based |


Cosmos DB is a superset of the Azure Table Storage functionality. You will choose Cosmos DB when you need multiple region redundancy, the highest throughput, minimal latency, or control of failover scenarios. You can learn more about the differences between Azure Table Storage and Cosmos DB, along with the Table API [here](https://docs.microsoft.com/en-us/azure/cosmos-db/table-introduction). 

Thanks for reading and until next time! MC signing off. 

**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.