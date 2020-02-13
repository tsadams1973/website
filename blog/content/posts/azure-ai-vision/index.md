---
title: "Computer Vision using Azure Cognitive Services"
date: 2020-02-13
draft: false
type: "post"
description: "A quick introduction to recognizing analyzing the content in images using python and azure."
tags: ["ai","azure","vision","cognitiveservices", "python"]
---

As part of my effort to learn more about artificial intelligence, machine learning, and Azure, I have been reading [Deep Learning with Azure](https://www.apress.com/gp/book/9781484236789). Having just finished **Part II: Azure AI Platform and Experimentation Tools**, I thought I might write up my experiences working with [computer vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) and [custom vision](https://azure.microsoft.com/en-us/services/cognitive-services/custom-vision-service/) while they are still fresh in my mind.

---

Despite the majority of my professional programming experience being in C#, I decided to use [Python](https://www.python.org/) to work through the examples. Given its popularity in the data science and machine learning communities, it made sense to me to get some more practice with it. With [Visual Studio Code](https://code.visualstudio.com/) being my preferred editor, the first step was to set it up for Python development.

#### Setting up Visual Studio Code for Python Development

Assuming you already use VS Code, Microsoft provides a [good tutorial](https://code.visualstudio.com/docs/python/python-tutorial) on how to get started using it with Python. Step one was to install the [Python extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-python.python). I chose to use[Anaconda](https://www.anaconda.com/distribution/) to manage my environments, so step two was to install it.

The step installing Anaconda is the main reason I'm including this part. First, given that I use a Mac and have recently upgraded to [macOS Catalina](https://www.apple.com/macos/catalina/), I also started using *[ZSH](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)* as my default shell instead of *bash*. So, while Anaconda installed correctly, and the application worked, I had trouble with using *conda* in the terminal.  I received the error:

```zsh
zsh: command not found: conda
```

After some searching I found some help on-line. The two primary sources I used were this [Medium article](https://towardsdatascience.com/how-to-successfully-install-anaconda-on-a-mac-and-actually-get-it-to-work-53ce18025f97) and this [post from the Anaconda team](https://www.anaconda.com/how-to-restore-anaconda-after-macos-catalina-update/). The solution that worked for me was to run this from the terminal:

```zsh
eval "$(/{your-path-here}/conda shell.zsh hook)”
conda init zsh
```

After that, *conda* worked as expected from the command line. And now you should be ready to work with Python using VS Code, which means you are also ready to work through the computer vision examples.

#### Computer Vision

Computer Vision is one of the AI services found under Microsoft's Cognitive Services. It analyzes the content found in images. If you scroll down on [this page](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) you can see it in action using a simple tool. You can easily create a new computer vision service from the [Azure portal](https://portal.azure.com) (see *Figure 1* and *Figure 2* below).

{{< imgproc azure-ai-1 Resize "600x" "Computer Vision" "Figure 1" />}}

{{< imgproc azure-ai-2 Resize "600x" "Computer Vision" "Figure 2" />}}

Once you create the service you can navigate to the *Quick start* tab under the *Resource Management* section of its blade to find some useful information. First, it will show you the *api key* and *endpoint* you will need to work with the service. Then it will show you two ways to try it out.

The first option is to navigate to the Cognitive Services [API Console](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa). (Make sure to copy your *api key* and note the location that you created your service in, you will need them.) From the API Console you can click the region for your service and then submit calls to see how the api works and what it returns. If you need some images to submit, I found this site useful: [free-images.com](https://free-images.com/). Once you are familiar with how the API operates, you can go back to the *Quick starts* in the portal to learn how to work with it using the custom vision client library for Python.

Microsoft has created a [simple tutorial](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/quickstarts-sdk/python-sdk) to show how the computer vision client library works. It includes all of the code you need to set up your environment and analyze images. If you'd rather just download the complete code, you find the official code on GitHub [here](https://github.com/Azure-Samples/cognitive-services-quickstart-code/tree/master/python/ComputerVision), or see my example [here](https://github.com/tsadams1973/python/blob/master/quickstart-file.py).

A few notes. First, since I was using *conda* to manage my environment, I also wanted to use that to set my environment variables. The code in the samples stays the same, but the [process to set up the variables](https://docs.microsoft.com/en-us/azure/cognitive-services/cognitive-services-apis-create-account?tabs=multiservice%2Cunix#configure-an-environment-variable-for-authentication) is different from what is listed in the tutorial. I found [this guide](https://towardsdatascience.com/how-to-hide-your-api-keys-in-python-fb2e1a61b0a0) useful to set it up, or you can refer directly to the [conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#macos-and-linux). In addition to setting up the environment variables, I also had to [install Pillow](https://pillow.readthedocs.io/en/stable/installation.html) in my environment. But after that, you should be able to use computer vision to analyze any images you would like.

#### Custom Vision

Custom Vision is also an AI Cognitive Service. It is an end-to-end platform built on computer vision that let's you create a train custom models tailored to your needs. Like the computer vision service, you can create this in the Azure portal as well (see *Figure 3*). Make sure to use the free tier if this is just for development and testing.

{{< imgproc azure-ai-3 Resize "600x" "Custom Vision" "Figure 3" />}}

After you create this, you will see two new services in your resource group: one for training and one for prediction. Opening either and looking at the *Quick start* option in its blade will give you some useful information to get started.

First thing to know is that custom vision includes its own [portal](https://www.customvision.ai/) that you can use to create and train your own models visually. It is a good idea to go sign in to that portal. Although we will be using the Custom Vision Python SDK to create our project, we will use the portal to examine it afterwards.

You will find a link to a [Quickstart: Create an image classification project with the Custom Vision Python SDK](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/python-tutorial) tutorial. Like the previous tutorial, you can find all of the code on that page, but if you'd like to, you can find the complete code that I used [here](https://github.com/tsadams1973/python/blob/master/custom-vision.py). (I only deviated from the code in the tutorial by including environment variables for the keys, endpoints, and paths as discussed above.) Another thing to note if you are running through the tutorial is that you will need to download the images from [this repo](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples/tree/master/samples/vision/images) to train the model. After that you should be able to run the sample code and see some output like that in *Figure 4*.

{{< imgproc azure-ai-4 Resize "300x" "Custom Vision" "Figure 4" />}}

After that you can go back to [customvision.ai](https://www.customvision.ai/) to explore your project visually. You can see it in the portal as in *Figure 5* below, and then explore some of its properties (or retrain it, etc.) as in *Figure 6*.

{{< imgproc azure-ai-5 Resize "600x" "Custom Vision" "Figure 5" />}}

{{< imgproc azure-ai-6 Resize "600x" "Custom Vision" "Figure 6" />}}

---

This is just the most basic introduction to using the Azure Vision Cognitive services, but hopefully it has helped you start to see what is possible and encouraged you to explore.
