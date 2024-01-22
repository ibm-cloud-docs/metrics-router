---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}



# About endpoints
{: #endpoints_about}

You can configure your account to manage private and public endpoints by using the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and Terraform scripts.
{: shortdesc}

You can view the type of endpoints that are available in the account to manage {{site.data.keyword.metrics_router_full_notm}} by using the [settings API](/docs/metrics-router?topic=metrics-router-settings).
{: tip}

## Private endpoints
{: #endpoints_about_private}

By default, private endpoints are enabled.

- You cannot disable private endpoints.

- The private endpoint format is `https://private.<region>.metrics-router.cloud.ibm.com/api/v3`.

- For more information about the list of `ENDPOINTS` that is available, see [Private endpoints](/docs/metrics-router?topic=metrics-router-endpoints#endpoints-api-metrics-router-private).

To manage {{site.data.keyword.metrics_router_full_notm}} in your account by using private endpoints only, see [Enforcing private endpoints to configure {{site.data.keyword.metrics_router_full_notm}} resources](/docs/metrics-router?topic=metrics-router-endpoints-enforce-private&interface=cli).

## Public endpoints
{: #endpoints_about_public}

By default, public endpoints are enabled.

You can disable the use of public endpoints to manage {{site.data.keyword.metrics_router_full_notm}} in your account by using private or public endpoints.

After public endpoints are disabled, you can enable public endpoints only by using the private endpoints.
{: important}

The public endpoint format is `https://<region>.metrics-router.cloud.ibm.com/api/v3`.

For more information about the list of `ENDPOINTS` that is available, see [Public endpoints](/docs/metrics-router?topic=metrics-router-endpoints#endpoints-api-metrics-router-public).
