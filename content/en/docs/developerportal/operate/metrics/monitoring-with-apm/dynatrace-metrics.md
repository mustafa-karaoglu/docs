---
title: "Dynatrace for the Mendix Cloud"
url: /developerportal/operate/dynatrace-metrics/
weight: 25
description: "How to configure Mendix Cloud v4 to enable monitoring and analysis with Dynatrace."
tags: ["Dynatrace", "Mendix Cloud", "v4", "monitoring", "analysis"]
#To update these screenshots, you can log in with credentials detailed in How to Update Screenshots Using Team Apps.
---

## 1 Introduction

[Dynatrace](https://www.dynatrace.com/) is a monitoring and analysis tool for cloud applications, providing monitoring of servers, databases, tools, and services through a SaaS-based data analytics platform. This document explains how to configure your Mendix Cloud v4 app to send data to Dynatrace to provide additional monitoring.

{{% alert color="info" %}}
Dynatrace is fully supported in Mendix version 9.7 and above.
{{% /alert %}}

For more information on the data you can send to Dynatrace, see [Monitoring Your Mendix Apps with an APM Tool](/developerportal/operate/monitoring-with-apm/).

## 2 Prerequisites

To use Dynatrace, and to send data to Dynatrace from your Mendix app, you will need the following:

* Access to a Saas or Managed Dynatrace environment
* The following information about Dynatrace
    * The Dynatrace environment url
    * An access token for integrating your Dynatrace environment with your Mendix app — you can find out how to obtain this in the Dynatrace documentation [Generate an access token](https://www.dynatrace.com/support/help/get-started/access-tokens#create-api-token)
* A licensed Mendix app of which you are the [Technical Contact](/developerportal/collaborate/app-roles/#technical-contact)

## 3 Connect Node to Dynatrace{#connect-node}

To send your runtime information to Dynatrace, you need to set it up using environment variables in the Developer Portal.

1. Go to the **Environments** page of your app in the *Developer Portal*.
2. Click **Details** to select the environment you wish to monitor with Dynatrace. 
3. Open the [**Runtime** tab](/developerportal/deploy/environments-details/#runtime-tab).
4. Add the following **Custom Environment Variable**s.

    1. DT_SAAS_URL – *Required*

        The url of Dynatrace environment. 

        The format for using the Dynatrace SaaS environment is similar to `https://<your-environment-id>.live.dynatrace.com`

        The format for using a Dynatrace managed environment is similar to  `https://<your-domain>/e/<your-environment-id>`

    2. DT_PAAS_TOKEN – *Required*

        The access token for integrating your Mendix app with Dynatrace, [created on Dynatrace environment](https://www.dynatrace.com/support/help/get-started/access-tokens#create-api-token).

        The token must include the `Ingest metrics` scope.

5. Return to the **General** tab and *restart* your environment.

## 4 Additional Information{#additional-info}

### 4.1 Dimensions

If you use Dynatrace to monitor more than one app and environment you will need some dimensions to be able to tell which app or environment these metrics apply to. To identify the metrics for your app and environment in Dynatrace, Mendix provide some default dimensions. You can also add extra dimensions.

#### 4.1.1 Default Dimensions

Mendix attaches these default dimensions to metrics that are pushed to Dynatrace:

* app – Environment Id of your Mendix environment
* instance_index – Instance index that metrics belong to

#### 4.1.2 Extra Dimensions

{{% alert color="info" %}}
What Dynatrace calls "dimensions", other monitoring tools call "tags". The Mendix Developer Portal therefore refers to a "tag" when it is setting up a Dynatrace "dimension".
{{% /alert %}}

Extra dimensions can be set as tags in the Developer Portal. We recommend that you at least set the following tag:

* env:{environment_name} – this enables you to identify metrics sent from a particular environment so you can separate out production metrics from test metrics (for example, **env:accp**)

To set this tag, do the following:

1. Go to the **Environments** page of your app in the *Developer Portal*.
2. Click **Details** to select an environment you are monitoring with Dynatrace. 
3. Open the **Tags** tab.
4. Add a **Tag** – this is the string which is sent to Dynatrace as a dimension. See [Tags Tab](/developerportal/deploy/environments-details/#tags) in *Environment Details* for more information.
5. **Restart** the application.

Setting this value for your app means that all metrics from this environment of your app will have these tags. For example, the tags for mx.microflow.time.avg for this set of metrics include **env:accp**.

### 4.2 Dynatrace Issues

If you have any issues related to accessing Dynatrace, please contact their support here: [Dynatrace Support](https://one.dynatrace.com/hc/en-us/requests). You will need a Dynatrace account to request support.

## 5 Read More

* [Metrics](/developerportal/operate/metrics/)
