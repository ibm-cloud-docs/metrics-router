---

copyright:
  years:  2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Planning the account configuration
{: #planning}

Plan the account's {{site.data.keyword.metrics_router_full_notm}} configuration to manage metrics in the {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

| Step | Description | Link |
| ---- | -------------- | -------------- |
| **1** | **Location & Services**  \n Identify the locations where you can configure {{site.data.keyword.metrics_router_full_notm}} to manage metrics.  \n  \n Identify which services in those locations generate metrics that you can manage by using {{site.data.keyword.metrics_router_full_notm}}. | [link](#planning-0) |
| **2** | **Metadata**  \n Decide the location in your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.metrics_router_full_notm}} metadata is stored.  \n   \n Take into account any corporate or industry compliance requirements such as Financial Services validated locations, or EU-managed regions. | [link](#planning-1) |
| **3** | **Endpoints**  \n Decide whether public endpoints, private endpoints, or both are allowed to manage the {{site.data.keyword.metrics_router_full_notm}} configuration. | [link](#planning-2) |
| **4** | **Target locations**  \n Define the locations where an account administrator can configure targets to collect metrics.  \n  \n You can choose any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. | [link](#planning-3) |
| **5** | **Default targets**  \n Define 1 default target for each account to configure where metrics that are not explicitly managed in the account's routing rules are routed.  \n   \n Consider defining a second default target for each account when you want to collect the data in a backup location or account. | [link](#planning-4) |
| **6** | **Number and location of targets**  \n Define the targets where you plan to collect metrics based on your regulatory and corporate requirements. \nDefine service to service authorizations between the {{site.data.keyword.metrics_router_full_notm}} service and the {{site.data.keyword.mon_full_notm}} instances that you configured as your destination targets. | [link](#planning-5) |
| **7** | **Routing rules**  \n Define the routing rules that indicate how to route metrics in your acccount.  \n  \n Decide if you want to drop the collection of metrics in 1 or more regions. Check any compliance requirements to confirm that you can. | [link](#planning-6) |
{: caption="Table 1. Planning" caption-side="bottom"}

## Locations and services
{: #planning-0}

Check the regions where you operate and identify how you can manage those metrics in the account:
- Identify the locations where you can configure IBM Cloud Activity Tracker to manage metrics. Check [Locations](/docs/metrics-router?topic=metrics-router-regions).
- Identify which services in those locations generate metrics that you can route through {{site.data.keyword.metrics_router_full_notm}}. Check [Services generating metrics](/docs/metrics-router?topic=metrics-router-cloud-services-mr).

You can use {{site.data.keyword.metrics_router_full_notm}} to manage metrics at the account-level. {{site.data.keyword.metrics_router_full_notm}} can only route metrics that are generated in [supported regions](/docs/metrics-router?topic=metrics-router-regions). Other regions, where {{site.data.keyword.metrics_router_full_notm}} is not available, continue to manage metrics by using {{site.data.keyword.mon_full_notm}}.



## Metadata location
{: #planning-1}

Decide the location in your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.metrics_router_full_notm}} account configuration metadata is stored.

You can choose any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

You can define a primary metadata location and a backup metadata location. Once a primary location is set, you can change it to a different region but you cannot disable it.

You must define a primary metadata location in the account before you can configure destinations and rules to route metrics in the account.
{: important}


## Endpoints allowed
{: #planning-2}

You can use public endpoints, private endpoints or both to manage the {{site.data.keyword.metrics_router_full_notm}} account configuration.

Decide whether public endpoints, private endpoints, or both are allowed to manage the {{site.data.keyword.metrics_router_full_notm}} account configuration. For more information, see [Enforcing private endpoints to configure {{site.data.keyword.metrics_router_full_notm}} resources](/docs/metrics-router?topic=metrics-router-endpoints-enforce-private).

Configure private endpoints and disable public endpoints when you require to be Financial Services Validated.
{: tip}

## Target locations
{: #planning-3}

Define the locations where an account administrator can configure targets to collect metrics. You can choose any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

To enforce target locations in the account, you can configure the account settings and specify the locations that are allowed.
{: tip}

Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

The location of a target definition must be a supported location where {{site.data.keyword.metrics_router_full_notm}} is available. The target can configure a resource in the same account where the metrics are located or in a different account. In addition, the resource can be located in any region where that type of resource is supported in {{site.data.keyword.cloud_notm}}.

For each target that you define in the same account where metrics are generated, you must define a service to service authorization between the {{site.data.keyword.metrics_router_full_notm}} service and the {{site.data.keyword.mon_full_notm}} instance that you configured as your destination in the target. For more information, see [Managing authorizations to grant access between services](/docs/metrics-router?topic=metrics-router-iam-service-auth).

For each target that you define in a different account from the one where metrics are generated, you must define a service to service authorization in the account where the target resource is available  between the {{site.data.keyword.metrics_router_full_notm}} service and the {{site.data.keyword.mon_full_notm}} instance that you configured as your destination in the target. For more information, see [Managing authorizations to grant access between services](/docs/metrics-router?topic=metrics-router-iam-service-auth).

## Default targets
{: #planning-4}

You can define up to 2 default targets in the account.
- Each target collects metrics that are not explicitly managed in the account's routing rules.
- Each target must be defined in the account before you can configure it as default one in the account.
- If you define more than 1 default target, all default targets get a copy of the metrics that does not have a clearly defined routing rule to indicate where to route them in the account.

Define 1 default target per account to configure where metrics that are not explicitly managed in the account's routing rules are routed. Consider defining a second default target per account when you want to collect the data in a backup location or account.
{: tip}



## Number and location of targets
{: #planning-5}

Define the targets where you plan to collect metrics based on your regulatory and corporate requirements.

- You can have 1 target per region to collect metrics for that region. Use this option to reduce latency and network connectivity issues.

- You can have 1 target to collect metrics across the entire account.

- You can define targets within the account or in a different account.

For more information, see [Targets](/docs/metrics-router?topic=metrics-router-target).


## Routing rules in the account
{: #planning-6}


Define the routing rules that indicate how to route metrics in your account.

- Routes are global.

- You can define up to 4 routes per account.

- You can define 1 or more routes to configure how metrics across all regions in your account are collected and stored in 1 or more targets.

- For each route that you define, you can configure 4 rules. These rules are applied top down. When a rule is identified for a region, any follow up rules withing that route definition that apply to that region are not considered.

Decide if you want to drop the collection of metrics in 1 or more regions. Check any compliance requirements to confirm that you can.

 -To drop the collection of metrics in 1 or more regions, you can configure a route for those regions with no targets defined.

For more information, see [Routes](/docs/metrics-router?topic=metrics-router-routes).
