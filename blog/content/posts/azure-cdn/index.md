---
title: "How to use a custom domain with your Azure static site"
date: 2019-07-12T22:29:16-04:00
draft: false
type: "post"
description: "Using the Azure CDN Profile to map a custom domain to your site with https."
tags: ["azure"]
---

In a previous [post](../azure-site/) we looked at how to host your static site in azure blog storage. We stopped with a simple 'hello world' page. 

Unfortunately the default address for you site will be in the somewhat undesirable format <resource-name>.<zone>.web.core.windows.net. For this blog that is: [https://timblog.z19.web.core.windows.net/](https://timblog.z19.web.core.windows.net/). Obviously, we might to use a domain we already own. Fortunately, there are some options for this.

We will use an Azure CDN to configure our custom domain endpoint. We will use this option because it will allow us to map our domain to our Azure site, set up a custom SSL certificate for our site, and create a rewrite rule to redirect our traffic to https.

So, let's get started.

---

First we need to login to our Azure portal and navigate to the storage resource we created to host our site. Once you do, scroll down to the "Blob service" section and choose "Azure CDN". It should look something like this: {{< imgproc azure-cdn-1 Resize "800x" "Azure CDN 1" "Figure 1" />}}

We will choose the "Create new" option and give our CDN profile a name. For pricing tier we will need to choose "Premium Verizon" because that is the only one that currently supports the rewrite rules we need. We will choose a name for our CDN endpoint, and leave the origin hostname as the default provided which should be in the format <service-host-name>.blob.core.windows.net.

Once those options are set, we will click "Create" and wait for our new endpoint to propagate.

---

This should create two resources. 
- A CDN Profile
- An endpoint

If we navigate to the endpoint from our Azure resources list we should see something like this:
{{< imgproc azure-cdn-2 Resize "800x" "Azure CDN 2" "Figure 2" />}}

To finish setting up our site, we want to choose the "Origin" option under setttings. We will see a screen like this:
{{< imgproc azure-cdn-3 Resize "800x" "Azure CDN 3" "Figure 3" />}}


We want to change "Origin type" to custom, and enter the domain for our static site in the "Origin hostname" field (which should propagate that name to the "Origin host header" field automatically.) Save your work.

The documentation says that it might take up to 30 minutes for the changes to propagate, but in my experience it might take longer. Stay the course. You can check your endpoint hostname. Eventually it will redirect to your static site.

---

Once you are satisfied that your CDN is redirecting to your static site, then we can look to adding a custom domain.

To do this, you need to go to your domain host and add a CNAME record for the domain (or subdomain) that you want to use. My domain is hosted by InMotion, and looks like this:
{{< imgproc azure-cdn-4 Resize "800x" "CNAME mapping" "Figure 4" />}}

Once you've set up your CNAME record, you can navigate to your endpoint in your Azure portal and hit the "+ Custom Domain" link. (See Figure 2 if you need a reference.) This will pop up an option to add a "Custom hostname" for your "Endpoint hostname". Simply add the custom domain for which you created the CNAME record and click "Add".
{{< imgproc azure-cdn-5 Resize "800x" "Custom domain mapping" "Figure 5" />}}

---

Once Azure is finished creating the custom domain you will see it listed on your endpoint page overview page but the column "Custom HTTPS" will be set to *Disabled*. Since we want to enable https, click on the custom domain to bring up its properties screen.

We will set:
- "Custom domain HTTPS" to *On*
- "Certificate management type" to *CDN managed*

Click "Save".
{{< imgproc azure-cdn-6 Resize "800x" "SSL" "Figure 6" />}}
This part can take a long time. Read: hours or up to a day. So, be patient. Eventually this process will complete, and your certificate will be provisioned. At this point, your custom domain should be mapped to your site with SSL. You can now safely navigate to it with https.

*Note:* If this takes longer than 24 hours, you might need to do some troubleshooting.

---

Last step: Now navigate to your site using https, but if you try to navigate to it using http, you will get rejected with a warning similar to:
{{< imgproc azure-cdn-7 Resize "800x" "Error" "Figure 7" />}}
This is a less than ideal user experience, so we want to fix it. Fortunately with the "Premium Verizon" pricing tier we can redirect http traffic to https. We will do this by creating a rule.

First you need to navigate out of your "Endpoint" to the "CDN Profile" resource that you set up originally to start the process. Once there you will see a "Manage" option at the top of the overview page that you want to select. {{< imgproc azure-cdn-8 Resize "800x" "CDN Profile" "Figure 8" />}}

This should take you to a new page where you can choose the "Rules Engine" option under the "HTTP Large" menu item.
{{< imgproc azure-cdn-9 Resize "800x" "Rules Engine" "Figure 9" />}}

Name your rule "Redirect http to https". Configure it by setting "If" "Request Scheme" "HTTP", then "URL Redirect" "origin-path/(.*)" to Destination "https://%{host}/$1".

{{< imgproc azure-cdn-10 Resize "800x" "Rule" "Figure 10" />}}

Hit "Add". Give Azure some time to propagate your changes, and that is it. You should be done.

---

Congratulations. Now you should have your own static website running in Azure blob storage, and you should also have it mapped to the custom domain of your choice, with an SSL certificate, and some rewrite rules to provide a pleasant user experience.

In a future post I will cover using Visual Studio Code with [hugo]() to build a more interesting and professional site.

Thanks!
