---

copyright:
  years:  2023, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with {{site.data.keyword.metrics_router_full_notm}}
{: #getting-started}



Use {{site.data.keyword.metrics_router_full}} to configure the routing of platform metrics generated in your {{site.data.keyword.cloud_notm}} account.
{: shortdesc}

You can use {{site.data.keyword.metrics_router_full_notm}}, a platform service, to manage platform metrics at the account-level by configuring targets and routes that define where data points are routed. {{site.data.keyword.metrics_router_full_notm}} can only route metrics that are generated in [supported regions](/docs/metrics-router?topic=metrics-router-regions) by enabled services. Other regions, where {{site.data.keyword.metrics_router_full_notm}} is not available, continue to manage metrics by using [{{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started). For more information about {{site.data.keyword.metrics_router_full_notm}}, see [About {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-about).

![A diagram that shows a sample {{site.data.keyword.metrics_router_full_notm}} architecture.](/images/metrics-routing-ov.png "{{site.data.keyword.metrics_router_full_notm}} architecture sample."){: caption="Figure 1. {{site.data.keyword.metrics_router_full_notm}} sample architecture" caption-side="bottom"}

## Prerequisites
{: #getting-started-prereqs}

- [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

- [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

- You must have a userid with permissions to manage {{site.data.keyword.metrics_router_full_notm}}. For more information about IAM roles and how to assign them, see [Managing access with IAM](/docs/metrics-router?topic=metrics-router-iam) and [Assigning access to {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-iam-assign-access).

- To configure {{site.data.keyword.metrics_router_full_notm}} to route metrics to a {{site.data.keyword.mon_short}} instance, you must configure a service to service authorization. You do not have to provide credentials to {{site.data.keyword.metrics_router_full_notm}}.

   For information on configuring service to service authentiation, see [Managing authorizations to grant access between services.](/docs/metrics-router?topic=metrics-router-iam-service-auth)



## Step 1. Configure the account settings
{: #getting-started-step1}

Set these account settings to define where and how metrics are collected, routed, and managed in your account by using {{site.data.keyword.metrics_router_full_notm}}.

When you configure {{site.data.keyword.metrics_router_full_notm}} in your account, you can configure account settings such as metadata locations, type of endpoints that are allowed to manage the configuration, locations where targets can be defined, and default targets for collecting  metrics in regions that you have not explicitly configured how to route metrics. For more information, see [Configuring {{site.data.keyword.metrics_router_full_notm}} account settings](/docs/metrics-router?topic=metrics-router-settings).

Before you can configure targets and routes in the account, you must configure the primary metadata location that defines the region where all your {{site.data.keyword.metrics_router_full_notm}} resource definitions are stored.
{: important}

Run the following command to configure the primary metadata location:

```pre
ibmcloud metrics-router setting update --primary-metadata-region <REGION>
```
{: codeblock}

Where `<REGION>` is set to a supported region where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

Before setting the metadata location, check any compliance or industry regulations that apply to the data location.
{: tip}



## Step 2. Configure 1 target
{: #getting-started-step2}

A target defines where metrics are collected. For more information about targets, see [Understanding how targets work in your account](/docs/metrics-router?topic=metrics-router-target&interface=cli#target_behavior).

When you configure a target, you are defining the destination where you plan to send platform metrics that are collected in a region in your account.

Complete the following steps to configure a target:

1. Define a target where to route metrics.

    ```text
    ibmcloud metrics-router target create --name TARGET_NAME --destination-crn DESTINATION_TARGET_CRN [--region REGION]
    ```
    {: pre}

    Where

    `--name`
    : Defines the name to be given to the target.

    `--destination-crn`
    : Defines the CRN of the {{site.data.keyword.mon_full_notm}} instance where you plan to route the metrics. {{site.data.keyword.mon_full_notm}} targets are the only ones supported.

    `--region`
    : [Optional] Defines the region where the target definition is created. You can only specify a [supported region](/docs/metrics-router?topic=metrics-router-regions&interface=cli). Set this option if you want to create a target in a region and you are connected to a different one.

2. Define a service to service authorization between the {{site.data.keyword.metrics_router_full_notm}} service and the {{site.data.keyword.mon_full_notm}} instance that you configured as your destination in the target. For more information, see [Managing authorizations to grant access between services](/docs/metrics-router?topic=metrics-router-iam-service-auth).

## Step 3. Configure 1 route
{: #getting-started-step3}

A route defines the rules that indicate what metrics are routed in a region and where to store them. Routes are global under an account and are evaluated in all regions where {{site.data.keyword.metrics_router_full_notm}} is deployed. For more information, see [Understanding how routes work in your account](/docs/metrics-router?topic=metrics-router-routes&interface=cli#route_behaviour).

In this step, you will configure a route to redirect metrics to the target destination that you configured in the previous step.

Run the following command to create the route:

```text
ibmcloud metrics-router route create --name ROUTE_NAME  --rules RULES
```
{: pre}

Where

`--name ROUTE_NAME`
:   Defines the name to be given to the route.

`--rules RULES`
:   Defines a JSON formatted rule definition enclosed in single quotes. [Learn more](/docs/metrics-router?topic=metrics-router-route_rules_definitions&interface=cli).

After you configure a route, it might take up to 1 hour for the configuration to be enabled.
{: note}

For example, to create a route to send metrics generated in us-east to the target that you created in the previous step, run the following command.

```text
ibmcloud metrics-router route create --name "my-route" --rules '[{"action": "send", "targets":[{"id":"TARGETID"}], "inclusion_filters":[{"operand": "location","operator": "is","values": "us-east"}]}]''
```
{: pre}

Where `TARGETID` is the ID of the target that you created in the previous step.


## Step 4. Verify collection of metrics
{: #getting-started-step4}


After the target and the route is configured, you must verify that metrics are available.

[Launch the {{site.data.keyword.mon_full_notm}} UI](/docs/monitoring?topic=monitoring-launch) for the {{site.data.keyword.mon_short}} instance that you configured as your target, and explore the metrics.

<!--## Next
{: #getting-started-next}

Plan your account configuration. For more information, see [Planning your account configuration settings](/docs/metrics-router?topic=metrics-router-planning).-->
