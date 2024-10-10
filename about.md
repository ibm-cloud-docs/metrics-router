---

copyright:
  years:  2023, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}




# About {{site.data.keyword.metrics_router_full_notm}} in {{site.data.keyword.cloud_notm}}
{: #about}

{{site.data.keyword.metrics_router_full_notm}} is a platform service that you can use to configure the routing of platform metrics generated in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

You can use {{site.data.keyword.metrics_router_full_notm}}, a platform service, to manage metrics at the account-level by configuring targets and routes that define where data points are routed. {{site.data.keyword.metrics_router_full_notm}} can only route metrics that are generated in [supported regions](/docs/metrics-router?topic=metrics-router-regions) by enabled services. Other regions, where {{site.data.keyword.metrics_router_full_notm}} is not available, continue to manage metrics by using [{{site.data.keyword.mon_short}}](/docs/monitoring?topic=monitoring-getting-started). For more information about  {{site.data.keyword.metrics_router_full_notm}}, see [About {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-about).

{{site.data.keyword.metrics_router_full_notm}} is an IBM Cloud platform service that enables the routing of platform metrics to appropriate backend storage and analysis systems based on compliance needs.

Use {{site.data.keyword.metrics_router_full_notm}} to combine platform metrics from many regions into one monitoring instance or to segment platform metrics into multiple monitoring instances within a region as dictated by your operational requirements.
{: tip}

![A diagram that shows a sample {{site.data.keyword.metrics_router_full_notm}} architecture.](/images/metrics-routing-ov.png "{{site.data.keyword.metrics_router_full_notm}} architecture sample."){: caption="{{site.data.keyword.metrics_router_full_notm}} sample architecture" caption-side="bottom"}

## Configuring the account
{: #metrics-resources-config}

To configure {{site.data.keyword.metrics_router_full_notm}} in your account, you must define where metrics are routed and stored. You must configure 1 or more targets, and 1 or more routes. You must also configure the account settings.

- A target defines the resource and location where time series data is routed.  For more information, see [Targets](/docs/metrics-router?topic=metrics-router-target&interface=api).

- A route defines the rules that indicate where time series data is routed in your account. For more information, see [Routes](/docs/metrics-router?topic=metrics-router-routes&interface=api).

- The account settings configuration defines information such as default targets where metrics are collected in the account, type of endpoints that are allowed to manage the configuration, and allowed locations to store the data in the account. For more information, see [Account settings](/docs/metrics-router?topic=metrics-router-settings).

You can configure the following types of targets:

| Target                                      | Type                     | When to use |
|---------------------------------------------|--------------------------|------------|
| {{site.data.keyword.mon_full_notm}}         | `sysdig-monitor`         | Consolidate time series data to the region of your primary operations. |
{: caption="List of targets" caption-side="top"}


The following table outlines the locations where you can configure {{site.data.keyword.metrics_router_full_notm}} to collect and manage metrics:

| Geo                   | Region                   | {{site.data.keyword.metrics_router_full_notm}} |
|-----------------------|--------------------------|----------------------------------------------------|
| Asia Pacific        | Chennai (`in-che`)       | [No]{: tag-red} |
| Asia Pacific        | Tokyo (`jp-tok`)         | [Yes]{: tag-green} |
| Asia Pacific        | Sydney (`au-syd`)        |  [Yes]{: tag-green} |
| Asia Pacific        | Osaka (`jp-osa`)         | [Yes]{: tag-green} |
| Europe              | Frankfurt (`eu-de`)      | [Yes]{: tag-green} |
| Europe              | London (`eu-gb`)         | [Yes]{: tag-green} |
| North America       | Dallas (`us-south`)      | [Yes]{: tag-green} |
| North America       | Toronto (`ca-tor`)       | [Yes]{: tag-green} |
| North America       | Washington DC (`us-east`)   | [Yes]{: tag-green} |
| South America       | Sao Paulo (`br-sao`)     | [Yes]{: tag-green} |
{: caption="Supported locations" caption-side="bottom"}


## Features
{: #about-features}

- Consolidate time series data to the region of your primary operations

- Route time series data to one or multiple locations

- Improve your data residency compliance stature, keeping data at-rest within certain regions
