---
title: "Practical Automated Machine Learning on Azure"
date: 2020-01-15
draft: true
type: "post"
description: "Some thoughts about the book and resources to help get through it more easily."
tags: ["azure","machine learning","ai"]
---

I picked up [this book](http://shop.oreilly.com/product/0636920269885.do) to learn more about machine learning on Azure. While it is a good book, and one I would recommend, I found some of the hands-on sections challenging. I put together some resources to help anyone else that experiences those same difficulties. If you are reading this, then that might be you.

I thought Part I. of the book, an overview of machine learning and explanation of how it works, was clear. However, getting into the good stuff in Part II. Automated ML on Azure, I felt the authors jumped into some examples without always providing clear direction on where to get the sample code. As I figured that out and worked through the chapters, I put together some notes and resources that I think better match up with the content of the book. I have included those below, organized by chapter title.

This all assumes you already have an Azure subscription set up.

---

### Getting Started with Microsoft Azure Machine Learning nad Automated ML

After a brief introduction, this chapter jumps right into Azure to set up a machine learning environment. It starts by asking us to register resources providers for those services (found in the *Settings* section of your subscription). This is the first discrepancy I found. The book tells us to search for *'machinelearning'*, and to register the following:

* Microsoft.MachineLearning
* Microsoft.MachineLearningCompute
* Microsoft.MachineLearningServices
* Microsoft.MachineLearningModelManagement

However, the only resource providers currently available in my subscription were Microsoft.MachineLearning and Microsoft.MachineLearningServices (see *Figure 1* below).

{{< imgproc azure-pml-1 Resize "425x" "Azure CDN 1" "Figure 1" />}}

If you see the same thing, just know that the examples will still work if you only register those two services. The Key Vault and container resource providers should all be there. The next step is to create a Machine Learning service. Again, the book tells you to search for *'machine learning service workspaces'* in Azure, but this does not seem to be the case anymore. Instead, simply search for *'machine learning'* and choose that option as seen in *Figure 2* below. The remainder of the instructions on setting up the workspace should still be accurate.

{{< imgproc azure-pml-2 Resize "600x" "Azure CDN 1" "Figure 2" />}}

*Note* - in the upcoming sections you will need to use the **subscription id**, **resource group name**, **workspace name**, and **region** to configure the examples. You might want to take note of them now, or at least be aware that they can all be found in the *Overview* section of the workspace you just created.

After this initial setup in Azure, you are directed to set up [Azure Notebooks](https://notebooks.azure.com/). While that part is straightforward, the book then proceeds to walk through a sample. I found that confusing because it was not entirely clear where that example came from. I was able to track it down, but lost some time doing that. To help anyone else having the same trouble I created my own Azure Notebook to cover this chapter. 

To run it, I recommend you clone my [practical-machine-learning](https://notebooks.azure.com/tsa-adams/projects/practical-machine-learning) project into your own Azure Notebook account. Run the notebook named *Chap_3_Predictive_maintenance_NASA_sample.ipynb* to easily follow along with the rest of the chapter. Because I used a simpler version of the sample illustrated in the book, the figure for *"Instantiating the Azure Machine Learning Workspace"* will look slightly different, but everything else should be the same. The only modification you need to make is to substitute your **subscription id**, **resource group name**, **workspace name**, and **region** where noted in the sample (this is mentioned in the book as well). Also note: the cell shown in *Figure 3* is the one that triggers the Azure authentication.

{{< imgproc azure-pml-3 Resize "800x" "Azure CDN 1" "Figure 3" />}}

Also, the AutoMLConfig step will likely throw a warning about the inputs being deprecated as shown in *Figure 4*. This appears to be triggered by the *"X ="* input, but does not negatively impact the notebook.

{{< imgproc azure-pml-4 Resize "800x" "Azure CDN 1" "Figure 4" />}}

Other than that, you should be able to run the notebook and follow along with the book.

### Feature Engineering and Automated Machine Learning

Chapter 4 talks about preprocessing and feature engineering with Azure Machine Learning and wastes no time jumping into some examples. It also presupposes that you have a Jupyter notebook set up to work through the Nasa Predictive Maintenance sample. I put together a Notebook in my [practical-machine-learning](https://notebooks.azure.com/tsa-adams/projects/practical-machine-learning) project to help with this: *Chap_4_Predictive_maintenance_NASA_sample.ipynb*.

This notebook will look very similar to the one used in the last chapter, except for a few changes:

* It uses the *train_FD004* data set instead of *train_FD001*
* It uses a slightly different AutoMLConfig to match the one from the chapter
* It includes the utility print functions and code to run them on the generated models

Do not forget to substitute your **subscription id**, **resource group name**, **workspace name**, and **region** where noted, and as with the last chapter, you will receive a warning about deprecated inputs to you AutoMLConfig. With this notebook you should be able to follow along with the examples in the first half of the chapter focusing on **Auto-Featurization for Classification and Regressing**.

*Note* - at the end of this sample, you will look at the engineered features with two different commands shown in *Figure 5* below. If you receive a key error for *'datatransformer'*, check that you have *'preprocess'* set to *True* in the AutoMLConfig.

{{< imgproc azure-pml-5 Resize "800x" "Azure ML 5" "Figure 5" />}}

Apart from that potential gotcha, you should be able to make it through the first half of this chapter easily.

For the second half of the chapter, **Auto-Featurization for Time-Series Forecasting**, refer to the *Chap_4_auto-ml-forecasting-energy-demand-end2end.ipynb* Notebook also located in the my [practical-machine-learning](https://notebooks.azure.com/tsa-adams/projects/practical-machine-learning) project.



### Deploying Automated Machine Learning Models

### Classification and Regression
