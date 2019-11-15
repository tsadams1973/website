---
title: "Deploying and Configuring Infrastructure on Azure"
date: 2019-10-19T10:39:40-04:00
draft: false
type: "post"
description: "All about managing Azure resources."
tags: ["azure","certification","training","az-300"]
---

After passing the AZ-900 exam to earn my Azure Fundamentals certificate, I thought I would move on to earning my [Azure Solutions Architect Expert](https://www.microsoft.com/en-us/learning/azure-solutions-architect.aspx) certification as well. This requires passing two exams: the [AZ-300: Microsoft Azure Architect Technologies](https://www.microsoft.com/en-us/learning/exam-AZ-300.aspx) and the [AZ-301 Microsoft Azure Architect Design](https://www.microsoft.com/en-us/learning/exam-AZ-301.aspx).

These are my notes about Deploying and Configuring Infrastructure, part of the AZ-300 exam.

---

### Monitoring

**Azure Monitor** provides tools to collect and analyze telemetry data to help you manage the performance and availability of your resources and applications. 

{{< imgproc az-monitor-1 Resize "800x" "Azure Monitor" "Figure 1" />}}

Data collected by Azure Monitor are either metrics or logs. Metrics are numbers that describe a property of a system at a point in time. Logs are records of different kinds of data. Most Azure resources show some data from Azure Monitor in their overview pages. Logs can be queried using Log Analytics from the Azure Portal. Azure monitor collects metrics, activity logs, and diagnostic logs:

* Application monitoring data
* Guest OS monitoring data
* Azure resources monitoring data
* Azure subscription monitoring data
* Azure tenant monitoring data

You can also use the Data Collector API to collect log data from REST clients to include them in your monitoring. With Application Insights you can monitor the availability, performance, and use of web applications (on-prem and cloud).

Azure monitor provides three capabilities:

* Monitor and visualize metrics
* Query and analyze logs
* Setup alerts and actions

The Activity Log is a subscription level log. Logs are kept for 90 days. It provides data on subscription level events from Azure Resource Manager through Service Health events. For any write operations it will tell you:

* What happened
* Who did it
* When it happened
* Current status
* The values of any other relevant properties

The activity log includes several types of events that may occur: administrative, service health, alert, autoscale, recommendation, security, and policy and resource health.

Azure Advisor makes recommendations to optimize your Azure usage for security, availability, performance, and cost. It will provide you with quick links to implement its suggestions or find more help about how to implement them.

### Alerts

Azure Monitor also provides alerting capabilities to let you know when important things happen. Alerts have: rules, action groups, and monitor conditions. Alert rules capture the target of the alert. The monitoring conditions define the criteria for it. Action groups define the preferences for how the notification will be handled (.e. email, ITSM, Logic or Function App, Runbook, SMS, Voice, or Webhook). Alerts have states (new, acknowledged, close) that are set by the user after the alert is fired. Alerts have monitoring conditions that are set by the system.

{{< imgproc az-alerts-1 Resize "400x" "Azure Alerts" "Figure 2" />}}

The Alerts page shows a summary of alerts that were created over a specified time frame. Clicking on an alert will take you to its detail page with additional information, including a history of actions taken by the alert or changes made to it.

### Activity Logs and Log Analytics

The Activity Log provides an audit trail of the activities performed on your Azure resources. (It differs from a Diagnostic Log because it shows outside activity acting on the resource, rather than information about the operation of that resource.) The Activity Log is one section of the Monitor blade. Also, most Azure resources have an Activity Log section in their blades to show activity filtered to that resource. You can define custom filters for the logs and save them. Creating a Log Profile will allow you to configure how your log is exported (where it is sent, the event categories to be sent, which regions to export, or how it should be retained). 

Looking at the Log Analytics workspaces architecture, connected sources provide information to the Log Analytics Service which stores data in the OMS Repository. An Azure storage account can also be configured to collect Azure Diagnostics data and send it to the Log Analytics service. You can query your logs with a special query language. The main tables with data are: event, syslog, heartbeat, and alert. Queries are basically the name of the table with the data followed by pipes with commands.

```
Event
| where (EventLevelName == "Warning")
```

### Network Watcher

The Azure Network Watcher has tools to monitor, diagnose, view metrics, and enable logs for resources in an Azure virtual network. You can automate remote network monitoring, see network traffic, and diagnose VPN issues. Connection monitor monitors the communication between a vm and an endpoint. Network performance monitor looks at network performance between points in the network infrastructure to detect issues like traffic blackholing or routing errors. You can generate a visual diagram of the resources in your virtual network using the Topology capability of Network Watcher. Helpful diagnostics include IP FLow Verify, Next Hop, and VPN Diagnostics. Network Security Group Flow Logs let you view information about ingress and egress IP traffic through an NSG. (Logs are JSON.)

---

### Supporting Links

* [Azure Monitor Documentation](https://docs.microsoft.com/en-us/azure/azure-monitor/)
* [Azure Monitor Overview](https://docs.microsoft.com/en-us/azure/azure-monitor/overview)
* [Overview of Log Queries](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview)
* [Data Explorer Query Language](https://docs.microsoft.com/en-us/azure/kusto/query/)
* [Azure Friday Azure Monitor](https://channel9.msdn.com/Shows/Azure-Friday/Azure-Monitor/player)
* [Azure Advisor Overview](https://docs.microsoft.com/en-us/azure/advisor/advisor-overview)
* [Azure Advisor Cost Reduction](https://docs.microsoft.com/en-us/azure/advisor/advisor-cost-recommendations)
* [Overview of Alerts](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-overview)
* [Overview of the Activity Log](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/activity-logs-overview)
* [Connecting to Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/agent-windows)
* [Data Sources in Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/agent-data-sources)
* [Getting started with Log queries](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/get-started-queries)
* [Network Watcher](https://azure.microsoft.com/en-us/services/network-watcher/)
* [Troubleshoot connections with Azure Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-connectivity-portal)