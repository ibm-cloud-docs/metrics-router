---

copyright:
  years:  2022, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Scenarios (WIP)
{: #scenarios}

Check out these sample scenarios to learn how to set up your account so that you can manage auditing events by using {{site.data.keyword.atracker_full}}.
{: shortdesc}

- Forward your activity event data to {{site.data.keyword.cos_full_notm}} for {{site.data.keyword.cloud_notm}} Financial Services compliance. See [Financial Services (FS) Validated scenario](/docs/atracker?topic=atracker-scenarios#scenarios-1).

- Improve data residency compliance by keeping data at-rest within specific locations such as the EU-managed locations. See [EU-managed account scenario](/docs/atracker?topic=atracker-scenarios#scenarios-2).

- Consolidate {{site.data.keyword.atracker_short}} data to the account and region of your primary operations. You can also route auditing events to multiple locations. See [Enterprise account scenario](/docs/atracker?topic=atracker-scenarios#scenarios-3).

- Manage global events in an account and route them to the location of your choice. See [Global events scenario](/docs/atracker?topic=atracker-scenarios#scenarios-4).

- Route data to a Data Lake for analytics. See [Data lake scenario](/docs/atracker?topic=atracker-scenarios#scenarios-5).




## Financial Services (FS) Validated scenario
{: #scenarios-1}

Forward your activity event data to {{site.data.keyword.cos_full_notm}} for {{site.data.keyword.cloud_notm}} for Financial Services compliance.
{: note}

If you require a solution that is Finantial Services (FS) Validated, you can run your business in {{site.data.keyword.cloud_notm}} in any of the supported regions such as us-south, us-east, eu-de, and eu-gb.

Therefore, to configure {{site.data.keyword.atracker_short}} for your account, you must define your account settings, targets and routes as follows:

- You must set your account *Metadata region primary* setting to any of the supported FS validated regions in  {{site.data.keyword.cloud_notm}}. For example, you can set it to `us-east`.

- You must set your account *Permitted target region* to the set of FS Validated regions where you operate. For example, you can set it to: `us-south,us-east,eu-gb,eu-de`. This setting will prevent administrators from creating targets in non-allowed locations.

- You must set your account *Private api endpoint only* setting to only allow administrators to use private endpoints to manage the {{site.data.keyword.atracker_short}} configuration.

- You can define 1 or more targets of type `cloud-object-storage` to store your auditing events.

    You cannot define targets of type `logdna`.
    {: important}

    You can define a cloud-object-storage target in any of the permitted regions.

- You must define the *Default targets* setting to configure up to 2 default targets that are used to route auditing events that are not explicitly managed in the account's routing rules. For example, if you have an enterprise account, you can define 1 target in a different account to route auditing events from any child accounts in your Enterprise, and a local target in the account to keep a copy local to the account.

- You must define 1 route to configure the account to route global auditing events and location-based auditing events.

    For example, to capture auditing events across all supported locations in a single target within the account, you can define a route with the following rule:

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de",
            "eu-gb",
            "us-south",
            "us-east"
         ],
         "target_ids":[
            "<COS TARGET ID 1>"
         ]
      }
    ]
    ```
    {: codeblock}

    For example, to capture auditing events across all supported locations within the account and in a different account, you can define a route with the following rule:

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de",
            "eu-gb",
            "us-south",
            "us-east"
         ],
         "target_ids":[
            "<COS TARGET ID 1>",
            "<COS TARGET ID 2>"
         ]
      }
    ]
    ```
    {: codeblock}

For example, your account settings would look like:

```text
ibmcloud atracker setting get
OK
IBM Cloud Activity Tracker settings
Metadata region primary:                             us-east
Default targets:                                     [<COS TARGET ID 1>,<COS TARGET ID 2>]
Permitted target regions:                            [us-south,us-east,eu-gb,eu-de]
Private api endpoint only:                           true
API version:                                         2
```
{: screen}

and your targets would look like:

```text
ibmcloud atracker target ls
Listing IBM Cloud Activity Tracker targets for all regions...
OK
Name                       ID                                     Region   Type                   Service to Service Enabled   CreatedAt                  UpdatedAt
target-cos                 <COS TARGET ID 1>                      eu-de    cloud_object_storage   true                         2022-05-16T17:16:05.234Z   2022-05-16T17:16:05.234Z
target-cross-acc-cos       <COS TARGET ID 2>                      eu-de    cloud_object_storage   true                         2022-05-16T17:16:05.721Z   2022-05-16T17:16:05.721Z
```
{: screen}


## EU-managed account scenario
{: #scenarios-2}

Improve data residency compliance by keeping data at-rest within EU-managed locations.
{: note}

If you require a solution that is EU-managed compliant, you must run your business in {{site.data.keyword.cloud_notm}} in the Frankfurt (eu-de) region, which is the only supported location that is EU-managed compliant.

Therefore, to configure {{site.data.keyword.atracker_short}} for your account, you must define your account settings, targets and routes as follows:

- You must set your account *Metadata region primary* setting to `Frankfurt (eu-de)`.

- You must set your account *Permitted target region* to `eu-de`. This setting will prevent administrators from creating targets in non-allowed locations.

- You can set your account *Private api endpoint only* setting to specifiy whether you allow administrators to use public endpoints, private endpoints, or both. This setting indicate the type of endpoints that are allowed to manage the {{site.data.keyword.atracker_short}} configuration.

- You can define 1 or more targets of type `cloud-object-storage` or `logdna` to store your auditing events. These targets must be located in Frankfurt.

   You can define a cloud-object-storage target in Frankfurt to store auditing events for long term storage.

   You can define a logdna target in Frankfurt to allow administrators to graphically search, and monitor auditing events, as well as define alerts.

- You can define the *Default targets* setting to configure up to 2 default targets that are used to collect auditing events that are not explicitly managed in the account's routing rules. For example, you can configure a cloud-object-storage target and a logdna target. You can setup alerts in the logdna target to get notified when events that are generated in non-eu managed locations in your account are reported.

- You must define 1 route to configure the account to route global auditing events and location-based auditing events that are generated in Frankfurt to the targets specified in the routing rule.

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de"
         ],
         "target_ids":[
            "<COS TARGET ID>",
            "<LOGDNA TARGET ID>"
         ]
      }
    ]
    ```
    {: codeblock}



For example, your account settings would look like:

```text
ibmcloud atracker setting get
OK
IBM Cloud Activity Tracker settings
Metadata region primary:                             eu-de
Default targets:                                     [<LOGDNA TARGET ID>,<COS TARGET ID>]
Permitted target regions:                            [eu-de]
Private api endpoint only:                           false
API version:                                         2
```
{: screen}

and your targets would look like:

```text
ibmcloud atracker target ls
Listing IBM Cloud Activity Tracker targets for all regions...
OK
Name            ID                                     Region   Type                   Service to Service Enabled   CreatedAt                  UpdatedAt
target-logdna   <LOGDNA TARGET ID>                     eu-de    logdna                 -                            2022-05-16T17:03:00.968Z   2022-05-16T17:03:00.968Z
target-cos      <COS TARGET ID>                        eu-de    cloud_object_storage   true                         2022-05-16T17:16:05.721Z   2022-05-16T17:16:05.721Z
```
{: screen}




## Enterprise account scenario
{: #scenarios-3}

Consolidate {{site.data.keyword.atracker_short}} data to the account and region of your primary operations. You can also route auditing events to multiple locations.
{: note}

For example, if you have an Enterprise with multiple child accounts, you can run your business in {{site.data.keyword.cloud_notm}} across multiple regions such as us-south, us-east, eu-de, au-syd, and eu-gb.
- You run development in the us-south region.
- You run QA in the eu-gb region.
- You run production in the eu-de and us-east regions.
- You only allow private endpoints to operate in {{site.data.keyword.cloud_notm}}.
- You only want to collect auditing events from your production regions.

In this scenario, to configure {{site.data.keyword.atracker_short}} for your account, you must define your account settings, targets and routes as follows:

- You must set your account *Metadata region primary* setting to any of the supported {{site.data.keyword.atracker_short}} regions in  {{site.data.keyword.cloud_notm}}. For example, you can set it to `us-east`.

- You must set your account *Permitted target region* to the regions where you operate. For example, you can set it to: `us-south,us-east,eu-gb,eu-de`. This setting will prevent administrators from creating targets in non-allowed locations.

- You must set your account *Private api endpoint only* setting to only allow administrators to use private endpoints to manage the {{site.data.keyword.atracker_short}} configuration.

- You can define 1 or more targets of type `cloud-object-storage` or `logdna` to store your auditing events.

- You can define the *Default targets* setting to configure up to 2 default targets that are used to collect auditing events that are not explicitly managed in the account's routing rules. For example,  you can define 1 target in a different account and route auditing events from any child accounts in your Enterprise to this target. You can also define a local target in the account to keep a copy local to the child account.

- You must define 1 route to configure the account to route global auditing events and location-based auditing events.

    For example, to capture auditing events across all supported locations in a single target within the account, you can define a route with the following rule:

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de",
            "us-east"
         ],
         "target_ids":[
            "<COS TARGET ID 1>"
         ]
      }
    ]
    ```
    {: codeblock}

    Because you have defined default targets in the account configuration settings, auditing events that are not explicitly managed in the account's routing rules are routed to these default targets.

    To drop auditing events for the regions where you run development and QA, you can add the following rule:

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de",
            "us-east"
         ],
         "target_ids":[
            "<COS TARGET ID 1>"
         ]
      },
      {
         "locations":[
            "eu-gb",
            "us-south"
         ],
         "target_ids":[
         ]
      }
    ]
    ```
    {: codeblock}

    If what you need is to capture auditing events across all supported locations in the account that generates the events and also in a different account where you collect events from all your Enterprise accounts, you can define a route with the following rule:

    ```json
    [
      {
         "locations":[
            "global",
            "eu-de",
            "us-east"
         ],
         "target_ids":[
            "<COS TARGET ID 1>",
            "<COS TARGET ID 2>"
         ]
      }
    ]
    ```
    {: codeblock}

Your account settings would look like:

```text
ibmcloud atracker setting get
OK
IBM Cloud Activity Tracker settings
Metadata region primary:                             us-east
Default targets:                                     [<COS TARGET ID 1>,<COS TARGET ID 2>]
Permitted target regions:                            [us-south,us-east,eu-gb,eu-de]
Private api endpoint only:                           true
API version:                                         2
```
{: screen}

and your targets would look like:

```text
ibmcloud atracker target ls
Listing IBM Cloud Activity Tracker targets for all regions...
OK
Name                       ID                                     Region   Type                   Service to Service Enabled   CreatedAt                  UpdatedAt
target-cos                 <COS TARGET ID 1>                      eu-de    cloud_object_storage   true                         2022-05-16T17:16:05.234Z   2022-05-16T17:16:05.234Z
target-cross-acc-cos       <COS TARGET ID 2>                      eu-de    cloud_object_storage   true                         2022-05-16T17:16:05.721Z   2022-05-16T17:16:05.721Z
```
{: screen}


## Global events scenario
{: #scenarios-4}


Manage global events in an account and route them to the location of your choice.
{: note}

If you manage auditing events through {{site.data.keyword.atracker_short}} event search instances in the account, global events are automatically routed to the instance in Frankfurt. However, you can configure {{site.data.keyword.atracker_short}} to configure the {{site.data.keyword.atracker_short}} instance of your choice where you can manage global events.

For example,
- You run your business in {{site.data.keyword.cloud_notm}} across multiple regions such as us-south, us-east, ca-tor, au-syd, and br-sao.
- You want to collect global events in a different location from Frankfurt. Notice that Frankfurt is the location where global events are available if you configure {{site.data.keyword.atracker_short}} event search in the account to manage auditing events in the account.

In this example, to configure {{site.data.keyword.atracker_short}} for your account, you must define your account settings, targets and routes as follows:

- You must set your account *Metadata region primary* setting to any of the supported {{site.data.keyword.atracker_short}} regions in {{site.data.keyword.cloud_notm}}. For example, you can set it to `us-east`.

- You must set your account *Permitted target region* to the region where you want to define the target resource that indicates the {{site.data.keyword.atracker_short}} instance where global events are routed. Consider setting it to the same location as the metadata region.

- You must define 1 target of type `logdna` to store your global auditing events.

- You must not set a default target to allow the default flows that route events for all regions to continue routing auditing events to each {{site.data.keyword.atracker_short}} instance in each region.

- You must define 1 route to configure the account to route global auditing events to the {{site.data.keyword.atracker_short}} instance of your choice.

    For example, you can define a route with the following rule:

    ```json
    [
      {
         "locations":[
            "global"
         ],
         "target_ids":[
            "<LOGDNA TARGET ID 1>"
         ]
      }
    ]
    ```
    {: codeblock}

Your account settings would look like:

```text
ibmcloud atracker setting get
OK
IBM Cloud Activity Tracker settings
Metadata region primary:                             us-east
Default targets:                                     []
Permitted target regions:                            [us-east]
Private api endpoint only:                           false
API version:                                         2
```
{: screen}

Your target would look like:

```text
ibmcloud atracker target ls
Listing IBM Cloud Activity Tracker targets for all regions...
OK
Name                       ID                                     Region     Type                   Service to Service Enabled   CreatedAt                  UpdatedAt
target-logdna              <LOGDNA TARGET ID 1>                   us-east    logdna                 -                            2022-05-16T17:16:05.234Z   2022-05-16T17:16:05.234Z
```
{: screen}




## Data Lake scenario
{: #scenarios-5}

You can choose any of the following options to send auditing events to a data lake:

- Configure your account to route auditing events to {{site.data.keyword.atracker_short}} hosted event search instances. Stream the events to {{site.data.keyword.messagehub}}, and then, send them to a data lake. You can filter the data to be streamed to the data lake.

    Simplify the {{site.data.keyword.atracker_short}} hosted event search configuration so only 1 instance needs to be configured to feed auditing events to {{site.data.keyword.messagehub}}.
    {: note}

- Configure {{site.data.keyword.atracker_short}} in your account to route auditing events directly to an {{site.data.keyword.cos_full_notm}} data lake.

    Use this option for Financial Services Cloud workloads where end-to-end compliance is required.
    {: note}
