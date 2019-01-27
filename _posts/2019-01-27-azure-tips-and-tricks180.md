---
layout: post
title: "Azure Tips and Tricks Part 180 - Taking a peek at Azure Key Vault Part 1 of 2"
excerpt: "Learn how to use taking a peek at azure key vault part 1 of 2"
tags: [azure, app service, portal, resources]
share: true
comments: true
---
 
**NEW:** Get your copy of the BEST Azure Tips and Tricks of all time in this FREE [eBook](http://ebook.azuredev.tips) now!
{: .notice--primary}
 
## The Complete List of Azure Tips and Tricks
 
[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success}


## Taking a peek at Azure Key Vault Part 1 of 2
 
One of the more vexing problems for developers is securing access to other services used by their applications. Databases and other restricted resources need authentication, and your apps need to provide that, but how? Passwords within your code? (Un)encrypted configuration files? Certificate stores? Hardware? And who safeguards and manages these resources?

Addressing these concerns is the primary objective of [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/), a globally available service to store and manage three types of assets:

- Secrets - sensitive strings like passwords and database connection strings. You might store your application�s database password as a secret, for instance.
- Encryption keys - RSA or Elliptic Curve keys that you would use for cryptographic operations such as encrypting application data for transit or storage.
- Certificates - X.509 certificates that you may provision through Azure Key Vault or via other providers like DigiCert.

In this post, you're going to see how to create and manage a secret, but keys work in much the same way. Certificates are a little more complex, and in fact themselves used keys and secrets. Check out [Get started with Key Vault Certificates](https://docs.microsoft.com/en-us/azure/key-vault/certificate-scenarios) for more information specifically on certificates.

## Creating a Key Vault Account

Let's start by creating a new Key Vault service in the Azure portal. In the Create Key Vault blade (below), provide a unique name for your vault (which, as with most services, becomes an endpoint for invoking the service) and pick (or create) a resource group and a pricing tier. There are currently two tiers, Standard and Premium; the latter supports keys protected by a hardware security module (HSM). Use the standard option for this exercise.

<img style="border:3px solid #021a40" src="/files/create-kv.png">

Access to the Key Vault is managed via policies to which principals (like users and applications) can be assigned. By default, the user creating the vault is granted all permissions to keys, secrets, and certificates, but in practice you will grant more detailed policies to specific principals. 

<img style="border:3px solid #021a40" src="/files/create-kv-policy.png">

Indeed, across the three entities (keys, secrets, and certificates), there are 40 permissions that can be individually granted, thus supporting the [principle of least privilege](https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models).  For instance, a web API that is accessing SQL Server might have GET permission on the secrets store, but only members of the security team would have SET permission to modify the database password. That�s a simplistic example, so [here�s another scenario](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault#example) involving developers, the security team, and even auditors.

### Adding a Secret

On the left sidebar menu of the Key Vault blade in the Azure portal, you can easily create or import a secret, key, or certificate. Since we're just interested in a secret now, we simply provide a name-value pair and options to manage the window of accessibility to that secret. 

<img style="border:3px solid #021a40" src="/files/create-secret.png">

Once the secret is created, you'll notice that there is a bit more depth to this than a simple key-value pair. For each secret, a versioning history is automatically maintained, and through the Secret Identifier URI you can access any version of that secret. This provides a bit of an audit trail and can help implement policies to forbid reuse of actual or derived values of previous secrets.

<img style="border:3px solid #021a40" src="/files/kv-history.png">

Although the Azure portal is a convenient visual approach to interact with Key Vault, for most scenarios you will want to have a repeatable and isolated process for managing Key Vault. Supporting that are the [Azure CLI](https://docs.microsoft.com/en-us/azure/key-vault/quick-create-cli) and [PowerShell cmdlets](https://docs.microsoft.com/en-us/azure/key-vault/quick-create-powershell) as well as [integration with Azure Resource Manager (ARM) templates](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-keyvault-parameter). 
From the perspective of consuming secrets (as well as keys and certificates) from Key Vault within your applications, SDKs and libraries are available in [.NET](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.keyvault?view=azure-dotnet), [Java](https://docs.microsoft.com/en-us/java/api/overview/azure/keyvault?view=azure-java-stable), [Node.js](https://docs.microsoft.com/en-us/javascript/api/overview/azure/key-vault?view=azure-node-latest), and [Python](https://docs.microsoft.com/en-us/python/api/overview/azure/key-vault?view=azure-python), and, of course, 
you can use the [REST API](https://docs.microsoft.com/en-us/rest/api/keyvault/) from any programming environment that supports HTTP. We'll look at a small sample using the .NET SDK in the [next installment](https://www.michaelcrump.net/azure-tips-and-tricks181).


**ATTENTION:** Help shape the future of Azure Tips and Tricks by telling me what you'd like for me to write about! Help me help you by filling out this [quick survey.](http://survey.azuredev.tips)
{: .notice--primary}
 
## Want more Azure Tips and Tricks?
If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below.
