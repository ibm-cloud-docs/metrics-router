---

copyright:
  years:  2023, 2024
lastupdated: "2024-05-03"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Required actions for newly supported regions
{: #new_region_support}

{{site.data.keyword.metrics_router_full}} is planned to be supported in the br-sao, ca-tor, jp-osa, and jp-tok regions in June 2024. As a result, all existing customers need to evaluate their {{site.data.keyword.metrics_router_full_notm}} configurations and make any required changes.
{: shortdesc}

## Check whether you have the right permissions
{: #new_region_1}

Log in to the {{site.data.keyword.cloud_notm}} by using an ID with {{site.data.keyword.iamshort}} with [Administrator permissions.](/docs/metrics-router?topic=metrics-router-iam)

## Check whether the routing rules capture metrics for the new regions
{: #new_region_2}

With routing rules, you can change the destination (the target) where metrics flow based on the region of the metrics.

The routing rules determine which metrics are matched for routing. You can also exclude the inclusion_filters definition when you configure a route to route all metrics, or drop all metrics.

Run the command `ibmcloud mr route ls`.

This example shows a route where metrics from us-east are routed to a target.

```text
$ ibmcloud mr route ls
OK
Name:         new-route
ID:           a4544cc3-e593-4b3b-a4ab-674d78ec3caa
CRN:          crn:v1:bluemix:public:metrics-router:global:a/81de6380e6232019c6567c9c8dexxxxx::route:a4544cc3-e593-4b3b-a4ab-674d78ec3caa
Rule 0:       [[15030278-9eeb-404e-b7aa-be1e8e8690d6(mon-std-secure)], [[location, is, [us-east]]]]
Created At:   2024-03-13T15:52:25.983Z
Updated At:   2024-03-13T15:52:25.983Z
```
{: screen}

If you have a configuration similar to this example, where you specify the locations from where to route metrics, you need to add the newly supported regions to your configuration.

This example shows a route where all metrics are dropped.

```text
Route
Name:         new-route2
ID:           d97f8358-f66d-48e0-9399-f15e090f4b44
CRN:          crn:v1:bluemix:public:metrics-router:global:a/81de6380e6232019c6567c9c8de6dece::route:d97f8358-f66d-48e0-9399-f15e090f4b44
Rule 0:       [drop, []]
Created At:   2024-03-13T16:40:47.394Z
Updated At:   2024-03-13T16:40:47.394Z
```
{: screen}

If you have a configuration similar to this example, where all metrics are dropped, metrics generated in the new regions will also be dropped.

This example shows a route where all metrics are routed:

```text
$ ibmcloud at route ls
OK
Route
Name:         new-route1
ID:           98911386-9c06-4a2b-aa14-9ac41bd5f7e1
CRN:          crn:v1:bluemix:public:metrics-router:global:a/81de6380e6232019c6567c9c8dxxxxx::route:98911386-9c06-4a2b-aa14-9ac41bd5f7e1
Rule 0:       [[15030278-9eeb-404e-b7aa-be1e8e8690d6(mon-std-secure)], []]
Created At:   2024-03-13T16:38:21.417Z
Updated At:   2024-03-13T16:38:21.417Z
```
{: screen}

If you have a configuration that routes all metrics, then all of your metrics will be routed to that target when the new {{site.data.keyword.metrics_router_full_notm}} regions are enabled.

For more information about configuring routes, see [Managing routes.](/docs/metrics-router?topic=metrics-router-route-manage)
{: tip}




## Check whether a default target is configured in your account
{: #new_region_3}

If you do not have a route that is configured, check if you have a default target that is configured in your account.

The default target in the {{site.data.keyword.metrics_router_full_notm}} settings is the destination where metrics are sent if there are no routing rules that match an metric's region.

Run the command `ibmcloud mr setting get`.

The “Default targets” array shows up to 2 defined targets that receive metrics, if there is no match in the routing definition.

For example, this shows that there are no default targets configured.

```text
$ ibmcloud at setting get
OK
IBM Cloud Metrics Routing settings
Primary metadata region:              us-east
Backup metadata region:               Not Initialized
Default targets:                      []
Permitted target regions:             []
Private api endpoint only:            false
```
{: screen}

This example shows that a default target is configured.

```text
$ ibmcloud at setting get
OK
IBM Cloud Metrics Routing settings
Primary metadata region:              us-east
Backup metadata region:               Not Initialized
Default targets:                      [15030278-9eeb-404e-b7aa-be1e8e8690d6]
Permitted target regions:             []
Private api endpoint only:            false
```
{: screen}

For more information about defining targets, see [Managing targets](/docs/metrics-router?topic=metrics-router-target-manage).
{: tip}

If you have a default target defined, then metrics not matching your account’s routing rules will be routed to the default targets and you are not affected by this change.

If you do not have a default target defined, then continue to the next step.

## Define a default target
{: #new_region_4}

If your configuration does not include either a default target or an explicit rule for each region's metrics, then metrics for the missing regions will be delivered to the service default target. You can configure a default target with the command `ibmcloud mr setting update --default-target <target-id>` so that metrics not matching routing rules will be routed to the default target (`<target-id>`).

For example:

```text
$ ibmcloud mr setting update --default-targets 15030278-9eeb-404e-b7aa-be1e8e8690d6
Are you sure you want to update the IBM Cloud Metrics Routing settings for your account? [y/N]> y
OK
IBM Cloud Metrics Routing settings
Primary metadata region:              us-east
Backup metadata region:               Not Initialized
Default targets:                      [15030278-9eeb-404e-b7aa-be1e8e8690d6(mon-std-secure)]
Permitted target regions:             []
Private api endpoint only:            false

```
{: screen}
