---
title: "Practical Automated Machine Learning on Azure"
date: 2020-01-15
draft: false
type: "post"
description: "Some thoughts about the book and resources to help get through it more easily."
tags: ["azure","machine learning","ai"]
---

I picked up [this book](http://shop.oreilly.com/product/0636920269885.do) to learn more about machine learning on Azure. While it is a good book, and one I would recommend, I found some of the hands-on sections challenging. I put together some resources to help anyone else that experiences those same difficulties. If you are reading this, then that might be you.

I thought Part I., **Automated MachineLearning**, of the book, an overview of machine learning and explanation of how it works, was clear. However, getting into the good stuff in Part II. **Automated ML on Azure**, I felt the authors jumped into some examples without always providing clear direction on where to get the sample code. As I figured that out and worked through the chapters, I put together some notes and resources that I think better match up with the content of the book. I have included those below, organized by chapter title:

* [Chapter 3 - Getting Started with Microsoft Azure Machine Learning and Automated ML](#one)
* [Chapter 4 - Feature Engineering and Automated Machine Learning](#two)
* [Chapter 5 - Deploying Automated Machine Learning Models](#three)
* [Chapter 6 - Classification and Regression](#four)

This all assumes you already have an Azure subscription set up.

---

## Part II. Automated ML on Azure

### Getting Started with Microsoft Azure Machine Learning and Automated ML {#one}

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

### Feature Engineering and Automated Machine Learning {#two}

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

This Notebook is organized a little differently than the other three we worked with. All of the Azure set up is moved to the top, so simply run through all of those until you get to the *Data* section, which is where the book picks up. We read the data set directly from the project instead of getting it from the URL first, because I have already included it in the project (see *Figure 6*). After that step you should recognize all of the code snippets from the book and be able to follow along seamlessly.

{{< imgproc azure-pml-6 Resize "650x" "Azure ML 6" "Figure 6" />}}

That wraps up Chapter 4 on feature engineering.

### Deploying Automated Machine Learning Models {#three}

My experience was that deploying the model from the example in Chapter 5 was challenging. The good news is that this chapter points you to a [Notebook you can use to follow along](https://github.com/PracticalAutomatedMachineLearning/Azure/blob/master/notebook/Chap_5_Model_Deployment.ipynb). The bad is that I had trouble creating the image in that Notebook. I mostly encountered errors installing *'psutil'* due to *'gcc'* not being found whenever I tried to include azureml-train-automl (which is required to run the image and score with the model). You are welcome to try their example, but I created my own version: *Chap_5_Model_Deployment.ipynb* in the [practical-machine-learning](https://notebooks.azure.com/tsa-adams/projects/practical-machine-learning) project using the [recommended Model.Deploy() approach](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-troubleshoot-deployment) and everything seemed to work. Best I can tell this is due to the base image that is used, but I could be wrong about that.

Something else to note about his chapter: at this point we are creating Container Registries and Container Instances, which cost more than the other resources we have been using so far. The AzureML SDK will create a registry for your Machine Learning workspace if one does not already exist. So, you don't need to explicitly create one. However, if you are using this resource simply to learn, then you might want to delete the Container Registry when you are done (or if you plan to leave it idle for a few days).

The problem with this approach is that your Machine Learning workspace will retain a reference to that original registry. So, future attempts to create images with the SDK will fail because it will not be able to find the registry you deleted. However, with a little preparation you can avoid this. For me, I downloaded the template for my registry before I deleted it. You can accomplish this with the *Export Template* option in the *Settings* section of the container registry blade as seen in *Figure 7*.

{{< imgproc azure-pml-7 Resize "650x" "Azure ML 7" "Figure 7" />}}

Once you have downloaded the template, it is easy to recreate the registry. You can run the following two commands in an Azure Cloud Shell powershell session. The first will delete the registry while the second will recreate it from the template you specify. I upload the template file to the cloud shell to make it easier to reference and reuse.

``` python
az acr delete -n <registry-name>
New-AzResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile <path-to-template>
```

One last detail: if you drop the registry and re-add it, you will lose all the keys necessary to access it. Fortunately the Azure ml cli has a command to fix this: *sync-keys*. This is also easily run from an Azure Cloud Shell powershell session. If you have not yet installed the ml cli, then you first need to add that extension. You can see both commands below. (The *sync-keys* command is also helpful if you regenerate passwords for your container registry. Basically anytime the components of your workspace have trouble communicating, give this command a go.)

``` python
az extension add --name azure-cli-ml
az ml workspace sync-keys -g practical-ml-rg --subscription-id 3b825558-5a02-405c-ad03-c83db8f38b89 -w auto-ml
```

You could probably avoid the above by [using the REST APIs to manage Machine Learning Service workspace data](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-export-delete-data). But I have yet to work much with it.

With that out of the way, we can quickly review the chapter. It picks up right at the point where you run the AutoML experiment. It then shows you how to register the model with Azure and retrieve its identifier. The book also includes a quick code snippet that shows how to register a model that you retrieve from an external source. In this case that model is the MNIST Handwritten Digit Recognition ONNX model. I've included that example in my Notebook for completeness.

After this, the book demonstrates how to create the *score.py* file used to create the container image. There are some minor discrepancies between the text in the book, the example code shown, and the notebook, but these are minor and do not effect the result. After that step we look at the dependencies from our experiment and print them out along with their version numbers. At this point my Notebook diverges from the book.

I run the same code found in the book to substitute the actual model id into the *score.py* file, but rather than creating a *yaml* file for the conda dependencies, I follow the [example](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-troubleshoot-deployment) that I linked earlier to create my environment and dependencies:

``` python
from azureml.core.model import InferenceConfig
from azureml.core.environment import Environment
from azureml.core.conda_dependencies import CondaDependencies

# Create the environment
myenv = Environment(name="myenv")

# Enable Docker and reference an image
myenv.docker.enabled = True

myenv.inferencing_stack_version='latest'

conda_dep = CondaDependencies.create(conda_packages=['numpy','scikit-learn','lightgbm'], 
                                     pip_packages=['azureml-defaults','azureml-sdk[automl]','azureml-train-automl','pynacl==1.2.1'])
myenv.python.conda_dependencies=conda_dep

inference_config = InferenceConfig(entry_script=script_file_name, environment=myenv)

myenv.save_to_directory('.',True)
conda_dep.save_to_file('.')
```

Using that configuration, we deploy the model as seen below. Be aware this can take a long time.

``` python
from azureml.core.webservice import AciWebservice

service_name = 'automl-pred-maint-inf'

# deploy the model
aci_config = AciWebservice.deploy_configuration(cpu_cores=1, memory_gb=1)
aci_service = Model.deploy(workspace=ws,
                       name=service_name,
                       models=[model],
                       inference_config=inference_config,
                       deployment_config=aci_config,
                       overwrite=True)
aci_service.wait_for_deployment(show_output=True)
print(aci_service.state)
```

After those two steps, we pick up with the book again where it prints out the URI for the scoring function. The section on **Testing a Deployed Model** should work the same between the two, with only some minor differences in the code.

The next section of the book, **Deploying to AKS**, takes the same model we just pushed to ACI and shows how to deploy it to an AKS cluster. This is not included in the original Notebook, but I added this section to mine. To be consistent, I used the same *Model.deploy()* approach to push to AKS, versus the image deployment they use in the chapter, but the result should be the same:

```python
from azureml.core.webservice import AksWebservice, Webservice
from azureml.core.model import Model

aks_target = AksCompute(ws,"myaks")

# deploy the model
deployment_config = AksWebservice.deploy_configuration(cpu_cores = 1, memory_gb = 1)
aks_service = Model.deploy(ws, 
                           "myservice", 
                           [model], 
                           inference_config, 
                           deployment_config, 
                           aks_target)
aks_service.wait_for_deployment(show_output = True)
print(aks_service.state)
```

This was the first time I had done anything with AKS in this subscription, so I had some initial trouble creating the AKS cluster. The [important note here](https://docs.microsoft.com/en-us/azure/machine-learning/how-to-deploy-azure-kubernetes-service#create-a-new-aks-cluster) mentions that you need to choose an agent count and vm size that works out to at least 12 virtual CPUs. However, I had a quota on my subscription for that region that was limiting it to 10 virtual cores. I was able to request an increase to that limit through Microsoft support, which removed that obstacle. So, if you encounter the same trouble, don't be alarmed.

The chapter continues with **Swagger Documentation for the Web Service**. It walks you through how to add decorators to the *score.py* file we have been using in order to generate Swagger documentation for the API. Since the chapter includes a [link](https://github.com/dcstwh/AzureMachineLearningAutoMLBook/blob/master/examples/swagger.json) to the github repository with the resulting *swagger.json* file in it, you should be able to follow along.

Chapter 5 wraps up with some helpful advice on how to debug service failures, and with that it is on to the next.

### Classification and Regression {#four}

Chapter 6 starts out covering some machine learning fundamentals, particularly the differences between classification and regression as machine learning techniques as well as the types of problems they are intended to solve. It wastes no time introducing the German Credit Risk data set that is used for the classification problem (identifying credit risks) it uses as an example.

In a couple pages it will point out where to get the [sample Notebook](https://github.com/PracticalAutomatedMachineLearning/Azure/blob/master/notebook/Chap_6_Classification.ipynb) for the chapter. As with previous chapters, I've included that Notebook with some minor modifications to make it easier to follow along with in my [practical-machine-learning](https://notebooks.azure.com/tsa-adams/projects/practical-machine-learning) project. It is named *Chap_6_Classification.ipynb*.

If you want to run the German credit risk code snippet, just scroll about a quarter of the way down the Notebook. It is the first cell in the **Data Preparation* section. All this really does is give you a quick view of the data we will be working with for this example.

After some more foundational discussion about classification and regression algorithms, the chapter has a section on **Setting up the Azure Machine Learning workspace** meant to walk you through configuring the sample Notebook. I rewrote the **Preparing the Azure Machine Learning Workspace** of the Notebook in my project to set everything up the way we have with all of the other Notebooks so far. So, this section will not be aligned between the book and the Notebook, but running through the steps should leave you in the same place by the time the **Data Preparation** section begins.

For the rest of the chapter, we walk through reading the data set and examining it before training models with automated ML, selecting the best model, and testing it. All of the steps from the chapter are included in the sample notebook, so it should be easy to follow along. One note: in the book, they set the number of iterations at 30 in the AutoML config. I've changed that back to 10 in the interest of saving some time. Also, the example notebook on github had some additional steps in it for looking at the data which I've left in my Notebook. So, everything from the chapter is in the Notebook, but there is some bonus code as well.
