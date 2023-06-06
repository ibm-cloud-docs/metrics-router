---

copyright:
  years:  2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data
{: #mng-data}

To ensure that you can securely manage your data when you use {{site.data.keyword.metrics_router_full_notm}}, it is important to know exactly what data is stored and encrypted, and how you can delete any stored data.
{: shortdesc}



## What data is stored in {{site.data.keyword.metrics_router_full_notm}}
{: #mng-data-stored}

{{site.data.keyword.metrics_router_full_notm}} stores configuration data only.
{: note}

- Stores target definitions in the region where the target is defined, and in the primary and backup metadata locations that you configure in the account. For more information, see [targets](/docs/metrics-router?topic=metrics-router-target).
- Stores route definitions in the primary and backup metadata locations that you configure in the account. For more information, see [routes](/docs/metrics-router?topic=metrics-router-routes).
- Stores account settings in the primary and backup metadata locations that you configure in the account. For more information, see [settings](/docs/metrics-router?topic=metrics-router-settings-about).




## How your data is stored and encrypted
{: #data-storage}

### Configuration data
{: #mng-data-storage-config}

You can configure {{site.data.keyword.metrics_router_full_notm}} resources by using public and private endpoints.

To ensure that you have enhanced control and security over your data, your account must be virtual routing and forwarding (VRF) enabled and you must use private routes to {{site.data.keyword.cloud}} service endpoints. You must configure {{site.data.keyword.metrics_router_full_notm}} resources over a private network connection.
{: note}

{{site.data.keyword.metrics_router_full_notm}} stores the configuration of settings, targets and routes for your account.
- Connections use TLS/SSL encryption for data in transit. The current supported version of this encryption is TLS 1.2.
- The storage where the configuration is stored is encrypted with LUKS using AES-256.


### Metrics data
{: #mng-data-storage-metrics}

You can define 1 or more routing rules that define how metrics are routed in the account.
- Metrics data from an {{site.data.keyword.cloud_notm}} service to your target service in {{site.data.keyword.cloud_notm}} is secured via private connection. The connection supports TLS 1.2.
- You must define a service to service authorization to enable the {{site.data.keyword.metrics_router_full_notm}} service to send data to a {{site.data.keyword.mon_full_notm}} instance.

You can store metrics data to an {{site.data.keyword.mon_full_notm}} instance. You manage the instance and the data that is collected in the instance. For more information, see [Data security](/docs/monitoring?topic=monitoring-mng-data).


## Deleting your data
{: #mng-data-storage-delete}

### Configuration data
{: #mng-data-storage-delete-config}

{{site.data.keyword.metrics_router_full_notm}} stores configuration data only.

You can delete any route, and target by using the API, the CLI or terraform scripts.

To stop {{site.data.keyword.metrics_router_full_notm}} from routing data to the configured targets, complete the following steps:

1. Delete all the routes in the account . For more information, see [Deleting a route](/docs/metrics-router?topic=metrics-router-route-manage&interface=cli#route-manage-cli-delete).
2. [Remove any default targets](/docs/metrics-router?topic=metrics-router-target-default-reset).


To delete a target, you must delete the target definition. Check that the target is not configured in a route. If it is, update the route to remove it.

To delete completely all the configuration data of the account, complete the following steps:

1. Delete all the routes in the account. For more information, see [Deleting a route](/docs/metrics-router?topic=metrics-router-route-manage&interface=cli#route-manage-cli-delete).
2. Delete all the targets in the account. For more information, see [Deleting a target using the CLI](/docs/metrics-router?topic=metrics-router-target-manage&interface=cli#target-manage-cli-delete).
3. [Remove any default targets](/docs/metrics-router?topic=metrics-router-target-default-reset).
4. Open an IBM support ticket to request deletion of all your service metadata. For information about opening an IBM support ticket, or about support levels and ticket severities, see [Getting support](/docs/get-support).



### Metrics data
{: #mng-data-storage-delete-metrics}

To delete metrics data, check the target type instructions.

- For {{site.data.keyword.mon_full_notm}} instances, see [Deleting your data](/docs/monitoring?topic=monitoring-mng-data#data-delete).
