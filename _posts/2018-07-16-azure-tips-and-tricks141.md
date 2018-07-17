---
layout: post
title: "Azure Tips and Tricks Part 141 - Generate a Zip file from Azure Blob Storage Files"
excerpt: "Learn how to easily generate a Zip file from Azure Blob Storage Files"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List of Azure Tips and Tricks

[Available Now!](https://michaelcrump.net/azure-tips-and-tricks-complete-list/){: .btn .btn--success} 

## Generate a Zip file from Azure Blob Storage Files

You might have a task that pops up where you need to generate a zip file from a number of files in your Azure blob storage account. For 1 or 2 files, this may not be a problem but for 20-2000, you might want to find a way to automate this. 

One option is to zip the files directly to the output stream using the blob streams. If you do this it still means that you are routing the stream through the web server. 

To begin you will want a way work with zip easily. I used the latest version of [ICSharpZipLib](https://github.com/icsharpcode/SharpZipLib) and make sure you pull in the [Azure Storage library](https://www.nuget.org/packages/WindowsAzure.Storage). 

We'll setup our Storage Service which will read from the stream and get a reference to the blob we are currently looping through. 


```csharp
public void ReadToStream(IFileIdentifier file, Stream stream, StorageType storageType = StorageType.Stored, ITenant overrideTenant = null)
{
    var reference = GetBlobReference(file, storageType, overrideTenant);
    reference.DownloadToStream(stream);
}


private CloudBlockBlob GetBlobReference(IFileIdentifier file, StorageType storageType = StorageType.Stored, ITenant overrideTenant = null)
{
    var filepath = GetFilePath(file, storageType);
    var container = GetTenantContainer(overrideTenant);
    return container.GetBlockBlobReference(filepath);
}
```

Now we have one method that takes in a response stream and loops through all the files to generate our zip file. 

```csharp
public void ZipFilesToResponse(HttpResponseBase response, IEnumerable<Asset> files, string zipFileName)
{
    using (var zipOutputStream = new ZipOutputStream(response.OutputStream))
    {
        zipOutputStream.SetLevel(0); // 0 - store only to 9 - means best compression
        response.BufferOutput = false;
        response.AddHeader("Content-Disposition", "attachment; filename=" + zipFileName);
        response.ContentType = "application/octet-stream";

        foreach (var file in files)
        {
            var entry = new ZipEntry(file.FilenameSlug())
            {
                DateTime = DateTime.Now,
                Size = file.Filesize
            };
            zipOutputStream.PutNextEntry(entry);
            storageService.ReadToStream(file, zipOutputStream);
            response.Flush();
            if (!response.IsClientConnected)
            {
                break;
            }
        }
        zipOutputStream.Finish();
        zipOutputStream.Close();
    }
    response.End();
}
```

Another "quick and dirty" MVC sample can be found below. This sample specifies the file names and the zip file name. 

```csharp
public ActionResult Download()
{
    var cloudStorageAccount = new CloudStorageAccount(new StorageCredentials("account-name", "account-key"), true);
    var container = cloudStorageAccount.CreateCloudBlobClient().GetContainerReference("test");
    var blobFileNames = new string[] { "file1.png", "file2.png", "file3.png", "file4.png" };
    using (var zipOutputStream = new ZipOutputStream(Response.OutputStream))
    {
        foreach (var blobFileName in blobFileNames)
        {
            zipOutputStream.SetLevel(0);
            var blob = container.GetBlockBlobReference(blobFileName);
            var entry = new ZipEntry(blobFileName);
            zipOutputStream.PutNextEntry(entry);
            blob.DownloadToStream(zipOutputStream);
        }
        zipOutputStream.Finish();
        zipOutputStream.Close();
    }
    Response.BufferOutput = false;
    Response.AddHeader("Content-Disposition", "attachment; filename=" + "zipFileName.zip");
    Response.ContentType = "application/octet-stream";
    Response.Flush();
    Response.End();
    return null;
}
```




## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump){: .btn .btn--success} or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 