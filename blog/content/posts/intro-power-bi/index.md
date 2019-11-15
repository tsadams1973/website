---
title: "Introduction to Power BI"
date: 2019-11-14T16:12:33-05:00
draft: false
type: "post"
description: "How to use Power BI."
tags: ["powerbi","bi","analytics"]
---

To learn more about Power BI, I decided to work through some of the content from the [Create and use analytics reports with Power BI](https://docs.microsoft.com/en-us/learn/paths/create-use-analytics-reports-power-bi/) learning path from Microsoft's (Learn platform)[https://docs.microsoft.com/en-us/learn/]. These are my notes and takeaways from those modules.

---

### Introduction

Power BI consists of three elements: 

* Power BI Desktop - a Microsoft Windows desktop application
* Power BI Service - a SaaS service
* Power BI Apps - apps available on mobile devices

The general workflow of Power BI would involve creating a report using the Power BI Desktop, publishing it to the Power BI service, and sharing it so users can consume it using a Power BI Mobile App.

---

The basic building blocks of Power BI are:

* Visualizations
* Datasets
* Reports
* Dashboards
* Tiles

Using these fundamental elements we can create a variety of reports ranging from simple to complex.

**Visualizations** are things like charts, graphs, or maps; ways to visually represent data. They are a useful way to present data in a context that makes it easier to understand and interpret. 

**Datasets** are collections of data. They can be created from a single source or a combination of multiple sources. Power BI features *connectors* which make it easy to connect to data sources such as Excel, SQL Server, or Salesforce to extract and filter data for your dataset.

**Reports** are ways to collect and present your visualizations. They can be a single page or multiple pages.

**Dashboards** are pages from a report that you share with others. They are collections of visualizations with the important constraint that they fit on one page.

**Tiles** are what hold visualizations on a report or dashboard. Each visualization represents one tile.

In general, with Power BI you can build datasets that contain the information you need, and then use visualizations to create reports and dashboards that tell the story behind those data.

---

From the Power BI service you can create *apps*. Apps are just prepackaged reports you can use. To see some, start by going to the [Power BI portal](https://app.powerbi.com/home). (If you need to sign up for Power BI, you can find information on how to do that [here](https://docs.microsoft.com/en-us/power-bi/service-self-service-signup-for-power-bi).)

Once you are on your Power BI dashboard, and easy way to see apps in action is to click "*Get Data*" in the bottom left of the page:
{{< imgproc power-bi-1 Resize "800x" "Power BI Apps 1" "Figure 1" />}}

Follow that up by clicking the "*Samples*" link, which should take you to a page like this:
{{< imgproc power-bi-2 Resize "800x" "Power BI Apps 2" "Figure 2" />}}

Choosing the "*Sales and Marketing Sample*" will take you to a prebuilt report for showing sales and marketing data:
{{< imgproc power-bi-3 Resize "800x" "Power BI Apps 3" "Figure 3" />}}

---

### Power BI Desktop

Before we take a look at Power BI Desktop, you will need to download it. You can find information on that [here](https://powerbi.microsoft.com/en-us/downloads/). With Power BI installed, let's continue.

When you open Power BI Desktop, you should see something like this:
{{< imgproc power-bi-4 Resize "800x" "Power BI Desktop" "Figure 4" />}}

It should look familiar to anyone used to working with Microsoft products:

1. A *ribbon* across the top for handling most tasks
2. A large *canvas* to work on
3. Collapsible *panes* to the right for working with data

Take notice of the **Publish** button in the upper right hand corner. This is how you will publish your report to the Power BI service after you are done creating it.

To load data into Power BI Desktop, choose the *Get Data* option in the home ribbon. Power BI has a number of built in connectors to attach to the data source of your choice. If you are planning to import data from Excel, make sure that you format your data as a *table* first. For a few other tips on how to work with Excel as a data source in Power BI, check out the [Microsoft documentation](https://docs.microsoft.com/en-us/power-bi/service-excel-workbook-files).

Inside Power BI Desktop, you can use the **Power Query Editor** tool to transform the data you are importing. This tool will allow you to duplicate or edit columns to make your data easier to work with. You will need to *Apply* your changes for them to take effect.

In addition to transforming your data, you can also combine data from different sources. Working within the Power Query Editor you can add new sources of data with the *New Source* button. You can choose to *merge* or *append* that data to your existing query to combine it with the original source.






