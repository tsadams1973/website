---
title: "Azure Fundamentals"
date: 2019-10-10
draft: false
type: "post"
description: "Taking the AZ-900 exam to get certified on Azure Fundamentals"
tags: ["azure certification"]
---

I have decided to purse some Azure certifications to improve my understanding of the product and bolster my resume. I generally like to start these types of efforts at the beginning, which means revisiting the fundamentals to ensure I have a good foundation. So, for this particular journey that means starting with an [Azure Fundamentals certification](https://www.microsoft.com/en-us/learning/azure-fundamentals.aspx) by taking the AZ-900 exam.

To keep it interesting, I though I might takes notes on the process here as I work through the [free training](https://docs.microsoft.com/en-us/learn/paths/azure-fundamentals/) Microsoft provides.

---

The [Microsoft training](https://docs.microsoft.com/en-us/learn/paths/azure-fundamentals/) is broken down into the following modules:

**Module 1:** *[Cloud Concepts - Principles of cloud computing](https://docs.microsoft.com/en-us/learn/modules/principles-cloud-computing/index)*

*Summary:*  
This module starts off by introducting the idea of cloud computing as a utility, similar to electricity. Cloud providers typically offer compute power, storage, networking, and anlytics. Compute offerings include VMs, containers, or serverless options. Storage offerings can scale based on need. Cloud computing can be flexible and cost efficient. It is based on a pay-as-you-go model. Cloud resources can scale vertically (adding more CPU's or memory) or horizontally (adding more servers). Cloud resources are elastic, so they can scale up and down as needed. Cloud computing is also current, reliable, and secure. Cloud providers can help compliance with regulations and standards (includes a list of compliance offerings). Cloud spending will be operational expenses (OpEx) rather than the capital expenses (CapEx) of tradiational on-premise offerings. Cloud deployment models define where your resources are stored and how your customers interact with them. You can choose public cloud (everything in the cloud), private cloud (everything on premise), or hybrid (some things in the public cloud some in the private cloud) models. In addition to cloud deployment models, there are three types of cloud services: infrastructure-as-a-service (IaaS), platform-as-a-service (PaaS), and software-as-a-service (SaaS). IaaS is akin to renting hardware from a cloud provider to run your systems: but you are still responsible for managing the operating systems, etc. PaaS, on the other hand, is a complete environment into which you can deploy your applications. With SaaS you are basically using software in the cloud over the web on a subscriptions service. The module ends with a quick quiz (knowledge check) and a summary. Overall I found this module took about 46 minutes to complete, versus the 62 minutes Microsoft estimated.

**Modlue 2:** *[Core Cloud Services - Introduction to Azure](https://docs.microsoft.com/en-us/learn/modules/welcome-to-azure/index)*

Summary:  
This module introduces Azure, Microsoft's cloud computing platform. A quick video describes you to how Azure works at a high level, introducing the concept of virtualization with hypervisor, and the fundamental orchestrator and fabric controller architecture that powers Azure. A quick overview of Azure services lists the most commonly used: compute, networking, storage, mobile, databases, web, internet of things, big data, AI, and DevOps. You recieve a brief description of each of these services before jumping in to create your own website. This will be done in an App Service, which is an http-based service that you can use to host web-based solutions without needing to manage infrastructure. Following along with the tutorial, we activate our development sandbox, login to the [Azure Portal](https://portal.azure.com/), and create a resource. We choose 'WordPress' to create a WordPress app and hit 'Create'. The tutorial gives you some values to enter. Make sure to read all the steps first, because you need to create a new service plan. If you try to create the app using the pre-filled service plan, it will fail. Once everything is configured hit 'Create' and wait for your app to depoly. Once deployment is complete, go to your resource in the azure portal. The overview page will show you the URL for it. Follow that to see your WordPress site up and running. After launching our site, we are invted to revisit the app in the portal. Looking at the overview page, we can see some graphs about the usage of our site, number of requests, data-in and data-out, etc. If we wanted to scale-up our app service to handle more load, we can do this with the scale-up option found in the app service's settings. (This would involve choosing a different pricing tier than we set in the original congiuration.) Finally we learn a bit about Azure Cloud Shell, which is a browser based CLI for programatically managing your Azure resources. The module runs us through some commands to list different azure resources associated with our subscription and eventually start and stop our app service from the command line. Again, the module ends with a quiz and summary. Unlike the last module, I found this one took about 59 minutes to complete versus the Microsoft estimate of 36 minutes. I'm sure the extra time was spent on the hands-on exercises.


**Modlue 3:** *[Core Cloud Services - Azure architecture and service guarantees](https://docs.microsoft.com/en-us/learn/modules/explore-azure-infrastructure/index)*  
Summary:
*TBD*

**Modlue 4:** *[Create an Azure account](https://docs.microsoft.com/en-us/learn/modules/create-an-azure-account/index)*  
Summary:
*TBD*

**Modlue 5:** *[Core Cloud Services - Manage services with the Azure portal](https://docs.microsoft.com/en-us/learn/modules/tour-azure-portal/index)*  
Summary:
*TBD*

**Modlue 6:** *[Core Cloud Services - Azure compute options](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-compute/index)*  
Summary:
*TBD*

**Modlue 7:** *[Core Cloud Services - Azure data storage options](https://docs.microsoft.com/en-us/learn/modules/intro-to-data-in-azure/index)*  
Summary:
*TBD*

**Modlue 8:** *[Core Cloud Services - Azure networking options](https://docs.microsoft.com/en-us/learn/modules/intro-to-azure-networking/index)*  
Summary:
*TBD*

**Modlue 9:** *[Security, responsibility and trust in Azure](https://docs.microsoft.com/en-us/learn/modules/intro-to-security-in-azure/index)*  
Summary:
*TBD*

**Modlue 10:** *[Apply and monitor infrastructure standards with Azure Policy](https://docs.microsoft.com/en-us/learn/modules/intro-to-governance/index)*  
Summary:
*TBD*

**Modlue 11:** *[Control and organize Azure resources with Azure Resource Manager](https://docs.microsoft.com/en-us/learn/modules/control-and-organize-with-azure-resource-manager/index)*  
Summary:
*TBD*

**Modlue 12:** *[Predict costs and optimize spending for Azure](https://docs.microsoft.com/en-us/learn/modules/predict-costs-and-optimize-spending/index)*  
Summary:
*TBD*

---

#### AZ-900 Review

*TBD*