---
layout: post
title: "Azure Tips and Tricks Part 170 - SAP on Azure in Plain English Part 1 of 2"
excerpt: "Learn about SAP hosted on Azure"
tags: [azure, sap, portal, tipsandtricks]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}
 
## SAP on Azure in Plain English Part 1 of 2
 
In this series, I take a look at SAP coming from someone who hasn't used it before. 

* [Part 1 - This post]
* [Part 2 - Coming tomorrow]()

## SAP - A brief history lesson from 1973 - 2018

SAP, the world's third-largest software company, produces business applications including customer relationship management (CRM) and enterprise resource planning (ERP) solutions. Since its first product was released in 1973, the company has made major changes to its software to accommodate industry trends from mainframes through to cloud computing. 

In 2010, with a focus on cloud computing, SAP developed the new SAP HANA platform, which is built on a proprietary database engine and forms the foundation of all its latest offerings. In 2015, SAP launched S/4HANA, which is a Business Suite implementation on this HANA platform. Microsoft and SAP have partnered to provide a range of SAP solutions running in the Azure cloud.

### Tell me more about SAP on Azure?

Traditionally, SAP systems were designed to be hosted on-premises and required a significant hardware investment. Using Azure we support both the traditional NetWeaver-based and HANA-based solutions.

You can also run your SAP applications in Azure which features the broadest global footprint, the largest compliance portfolio, embedded security, enterprise-grade SLAs, and industry-leading support. Azure supports the largest SAP HANA workloads of any hyperscale cloud provider.

### What offerings are available?

Azure has a number of preconfigured (and SAP certified) virtual machine images, published by SAP and third-party Linux vendors, so that you can spin up your infrastructure in minutes rather than the weeks it would take on-premises. You can select from a wide range of virtual machine SKUs and even add your own license. Just search for **Marketplace** and click on **Compute** and filter by **SAP**.
 
<img style="border:3px solid #021a40" src="/files/azure-sap-vms.png">

The **SAP HANA express edition (Server + Applications)** image contains a full development image and will deploy to a D12v2 virtual machine. Storage and networking options are preconfigured to ensure you can quickly create a system that will support SAP HANA.

SAP HANA, express edition includes the in-memory data engine with advanced analytical data processing engines for business, text, spatial and graph data - supporting multiple data models on a single copy of the data The software license allows for both non-production and production use cases, enabling you to quickly prototype, demo and deploy next-generation applications with SAP HANA, express edition.
This image contains only the advanced data processing engines, without XSA stack, web based IDE and administration tools.

Below, I've started creating a VM using this template. If you are doing the same (just for testing) then you'll want to leave the **Size** as-is as dropping down to a **Basic A0** won't work. You want to make sure that the **Image** is **SAP HANA, express edition (Server + Applications)
 
<img style="border:3px solid #021a40" src="/files/azure-sap-create-vm.png">

It's important to note at this stage that these VMs are not available in all regions. If you select a region where the required machines are not available, the entry next to **Size** will be blank. You can skip straight to **Review + Create** at this point or customize options for disks, networking, etc. 

<img style="border:3px solid #021a40" src="/files/azure-sap-review.png">
 
After you hit **Create** on the review screen, you'll reach a status page showing the deployment in progress and finally when it has completed.

<img style="border:3px solid #021a40" src="/files/azure-sap-creation.png">

Come back tomorrow and we'll take a look at this VM and start setting everything up. 


**ATTENTION:** If you liked this post and want to suggest future topics of Azure Tips and Tricks then [complete this survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
 
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.