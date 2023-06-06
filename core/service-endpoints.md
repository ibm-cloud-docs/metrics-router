---

copyright:
  years:  2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Using service endpoints to privately connect to {{site.data.keyword.metrics_router_full_notm}}
{: #service-endpoints}

To add more control and security over your data when you use {{site.data.keyword.metrics_router_full}}, you have the option of using private routes to {{site.data.keyword.cloud_notm}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} Private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}



## Before you begin
{: #prereq-service-endpoint}


You can use private and public endpoints to configure {{site.data.keyword.metrics_router_full_notm}} resources in your account.

You can connect to {{site.data.keyword.metrics_router_full_notm}} over a private network by using {{site.data.keyword.cloud_notm}} Private service endpoints.
- When you use the classic infrastructure, you connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network by default. You can enable virtual routing and forwarding (VRF) to move IP routing for your account and all of its resources into a separate routing table. If VRF is enabled, you can then enable {{site.data.keyword.cloud_notm}} service endpoints to connect directly to resources without using the public network. [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).
- Virtual Private Clouds (VPCs) are automatically enabled for virtual routing and forwarding (VRF). To enable service endpoints for your VPC, continue to [Enabling service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).

To check whether the account is VRF enabled, run the following command:

```text
ibmcloud account show
```
{: pre}

To enable private endpoints, run the following command:

```text
ibmcloud account update --service-endpoint-enable true
```
{: pre}



## Setting up service endpoints for {{site.data.keyword.metrics_router_full_notm}}
{: #endpoint-setup}

By default, private and public endpoints are enabled. For more information about supported endpoints, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


## Disabling public service endpoints
{: #endpoint-disable}

You can disable public endpoints in your account for {{site.data.keyword.metrics_router_full_notm}}:
- If public and private endpoints are enabled, you can disable a public endpoint by using private or public endpoints.
- If public endpoints are disabled, you can enable public endpoints only by using the private endpoint.

For more information, see [Enforcing private endpoints to configure {{site.data.keyword.metrics_router_full_notm}} resources](/docs/metrics-router?topic=metrics-router-endpoints-enforce-private).


## Disabling private service endpoints
{: #endpoint-disable-private}

You cannot disable private endpoints.
