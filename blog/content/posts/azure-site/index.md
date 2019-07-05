---
title: "Host your website on Azure"
date: 2019-07-05T11:53:20-04:00
draft: false
type: "post"
description: "Using Azure blob storage to host your static website."
tags: ["azure"]
---

One useful feature of Microsoft Azure that has recently achieved general availability is the ability to host static websites in Azure storage. This blog is an example of such a site, so I thought I might put together a series of posts describing how I built and hosted it. This first installment will cover setting up a simple site in Azure.

I will assume that you already have a Microsoft Azure subscription, but if not you can get started with a free account here:
[Microsoft Azure Free Account](https://azure.microsoft.com/en-us/free/)

---

So, now that you have an Azure account set up, log in to your portal. Near the top of the left blade you should see an option to "Create a Resource". Click it and you will see something that looks like this:

{{< imgproc azure-1 Resize "600x" "Azure screen" "Figure 1" />}}

I will suggest that you search for "Storage account" in the search box (or you can scroll down the list to find it) and then click 'Create'.

You will be presented with some options. You can set these how you like but for the purposes of this walkthrough. You can accept all of the defaults here. I chose to:
 
- Create a new resource group called *test-static-site-rg*.
   
- Change the replication to *Locally-redundant storage (LRS)*.

{{< imgproc storage-create-2 Resize "600x" "Create Storage 2" "Figure 2" />}}

If your options look like this, then click "Create" and let's continue.

---

Once your new storage account has finished deploying to Azure, you will be albe to find it in your list of Azure resources. 

{{< imgproc storage-create-3 Resize "600x" "Create Storage 3" "Figure 3" />}}

If you scroll down the list of options on your storage account you will find one conveniently called "Static website". (If you have trouble finding it, simply search for it using the text box near the top of the options.) After choosing it, you will be presented with some text to the effect of *"Configuring the blob service for static website hosting enables you to host static content in your storage account. Webpages may include static content and client-side scripts. Server-side scripting is not supported in Azure Storage."*

Once you choose the "Enabled" option, you will see two new fields. Fill them out as follows:

 - Index document name: *index.html*

 - Error document path: *404.html*

 After you click "Save" you should see the following screen:

{{< imgproc storage-create-4 Resize "600x" "Create Storage 4" "Figure 4" />}}

After saving, Azure automatically created a *$web* container for you. The next step is to create and upload the *index.html* and *404.html* files we referenced earlier. You can either click on the *$web* link on the "Static website" properties page or find the "Blobs" option in the left menu and the click the *$web* link for the continer you find there. Either way, you end up here:

{{< imgproc storage-create-5 Resize "600x" "Create Storage 5" "Figure 5" />}}

---

Creating a website is a little ouf-of-scope for this post, although I plan to cover that in a follow-up. But, we need something to finish off this tutorial. So, use any editor you like and make two files on your local computer.

**index.html**
```
<html>
    <head></head>
    <body>
        <h1>Hello World.</h1>
        <p>
            My static website.
        </p>
    </body>
</html>
```

**404.html**
```
<html>
    <head></head>
    <body>
        <h1>File Not Found.</h1>
        <p>
            This page was not found.
        </p>
    </body>
</html>
```

Upload each of those to the *$web* container using the 'Upload' feature. Once the files are uploaded, navigate to the "Primary endpoint" for your site. The endpoint can be found under the "Static website" properties on the screen we saw in **Figure 4**. The endpoint will be in the format: <*resource-name*>.<*zone*>.web.core.windows.net.

You should see the simple *Hello World* page we uploaded.

---

That's it. You are now ready to add more content and style to your page. In a future post I will cover using Visucal Studio Code and a static site generator to develop a more interesting website.

Thanks.
