---

copyright:
  years:  2023, 2025
lastupdated: "2025-08-21"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.metrics_router_full_notm}}
{: #vpe-connection}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for VPC enables you to connect to {{site.data.keyword.metrics_router_full_notm}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and the {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

{{site.data.keyword.metrics_router_full_notm}} supports VPEs in Montreal (`ca-mon`) only.
{: restriction}

## Before you begin
{: #prereq-service-endpoint}

Before you target a virtual private endpoint for {{site.data.keyword.metrics_router_full_notm}} you must complete the following tasks.

* Ensure that a [Virtual Private Cloud is created](/docs/vpc?topic=vpc-getting-started).
* Make a plan for your [virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
* Ensure that [correct access controls](/docs/vpc?topic=vpc-configure-acls-sgs-endpoint-gateways) are set for your virtual private endpoint.
* Understand the [limitations](/docs/vpc?topic=vpc-limitations) of VPC.
* Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Setting up a VPE for {{site.data.keyword.metrics_router_full_notm}}
{: #endpoint-setup}

When you create a VPE gateway by using the CLI or API, you must specify the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the region in which you want connect to {{site.data.keyword.metrics_router_full_notm}}. Review the following table for the available regions and CRNs to use to create your VPE gateway.


| Region | Cloud Resource Name (CRN) |
|-----------------|-----------------|
| `ca-mon` | `crn:v1:bluemix:public:metrics-router:ca-mon:::endpoint:api.private.ca-mon.metrics-router.cloud.ibm.com` |
{: caption="Region availability and Cloud Resource Names for connecting {{site.data.keyword.metrics_router_full_notm}} over {{site.data.keyword.cloud_notm}} private networks" caption-side="bottom"}


### Configuring an endpoint gateway
{: #endpoint-gateway-servicename}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users.
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for {{site.data.keyword.metrics_router_full_notm}} that you want to be privately available to the VPC.
3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with {{site.data.keyword.metrics_router_full_notm}}. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.metrics_router_full_notm}} instance privately through it.

## Using your VPE for {{site.data.keyword.metrics_router_full_notm}}
{: #using-servicename-vpe}

After you create an endpoint gateway for {{site.data.keyword.metrics_router_full_notm}}, you can use the VPE with the VPC API.

### Using the VPE with the API
{: #vpe-api}
{: api}

After creating an endpoint gateway for the {{site.data.keyword.metrics_router_full_notm}} service, use the service endpoint's FQDN `api.private.<REGION>.metrics-router.cloud.ibm.com` in the URL to access the service. For example:

```sh
curl https://api.private.ca-mon.metrics-router.cloud.ibm.com/api/v3/targets' -H "Authorization: Bearer $iam_token"
```
{: pre}


### Using the VPE with the CLI
{: #vpe-cli}
{: cli}

After creating an endpoint gateway for the {{site.data.keyword.metrics_router_full_notm}} service, run the following command with the service endpoint's FQDN `api.private.<REGION>.metrics-router.cloud.ibm.com` to access the service. For example:

```sh
export METRICS_ROUTER_API_ENDPOINT=https://api.private.ca-mon.metrics-router.cloud.ibm.com/api/v3
```
{: pre}


### Using the VPE with Terraform
{: #vpe-terraform}
{: terraform}

After creating an endpoint gateway for the {{site.data.keyword.metrics_router_full_notm}} service, run the following command with the service endpoint's FQDN `api.private.<REGION>.metrics-router.cloud.ibm.com` to access the service. For example:

```sh
export IBMCLOUD_METRICS_ROUTING_API_ENDPOINT=https://api.private.ca-mon.metrics-router.cloud.ibm.com/api/v3
```
{: pre}
