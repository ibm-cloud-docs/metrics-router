---

copyright:
  years:  2022, 2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Configuring account settings
{: #settings-about}

You can configure your account settings for {{site.data.keyword.metrics_router_full}} by using the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and Terraform scripts. Set these settings to define where and how metrics are collected, routed, and managed in your account.
{: shortdesc}

When you configure or modify the {{site.data.keyword.metrics_router_full_notm}} account settings, consider the following information:

- Every time you modify the {{site.data.keyword.metrics_router_full_notm}} account settings, the data that is passed in the new request replaces any existing configuration data. You must ensure that any existing data is not deleted when you run an update of the account settings by including it in the new request.
{: important}

- Before you disable public endpoints by setting `--private-api-endpoint-only TRUE`, make sure your account has access to the private endpoint.  You can do this by running the command `ibmcloud account show`.  If `VRF Enabled` is `true` and `Service Endpoint Enabled` is `true` then you have access to the private endpoint.  If you do not have access to the private endpoint, you will be unable to re-enable the public endpoint since private endpoint access is required to re-enable the public endpoint.
{: important}

- You can use private and public endpoints to manage settings. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/metrics_router?topic=metrics_router-endpoints).

    Through the private network, you must use an API endpoint with the following format: `https://private.<region>.metrics_router.cloud.ibm.com`

    Through the public network, you must use an API endpoint with the following format: `https://<region>.metrics_router.cloud.ibm.com`


## What data can you configure through the {{site.data.keyword.metrics_router_full}} account settings?
{: #settings-about-what}

You can define any of the following information:

*  The location in your {{site.data.keyword.cloud_notm}} account where the {{site.data.keyword.metrics_router_full_notm}} account configuration metadata is stored.

    By metadata, we refer to the target/route/settings data that is available across the account in any region.

    You can choose any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics_router?topic=metrics_router-regions&interface=cli).

    You can choose a location where the data is stored. You can also configure a backup location where the metadata is stored for recovery purposes.

    Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

    If you do not configure the primary metadata region, the location of the first target that you configure in the account determines the primary metadata location.

* The type of endpoints that are allowed to manage the {{site.data.keyword.metrics_router_full_notm}} account configuration in the account.

    By default, public and private endpoints are enabled.

    You can configure your account to restrict management through private endpoints only.

* The locations where an account administrator can define targets to collect metrics.

    You can choose any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics_router?topic=metrics_router-regions&interface=cli).

    Take into account any corporate or industry compliance requirements such as Financial Services Validated locations, or EU-managed regions.

* Default target locations, that is, 1 or more targets in the account, that will collect metrics from supported {{site.data.keyword.metrics_router_full_notm}} locations where you have not configured how you want to collect metrics.

   If you define more than 1 target, all default targets get a copy of metrics that do not have a routing rule to indicate where to collect them in the account. You can define up to 2 default targets per account.
   {: note}



## IAM permissions
{: #settings-about-access}

Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}} settingss.](/docs/metrics-router?topic=metrics-router-iam)




## CLI commands
{: #settings-about-cli}

The following table lists the actions that you can run to manage settings:

| Action                     | Command                                         |
|----------------------------|--------------------------------------------------|
| Get settings information   | `ibmcloud metrics-router setting get`        |
| Update settings            | `ibmcloud metrics-router setting update`   |
{: caption="Table 1. Settings actions by using the {{site.data.keyword.metrics_router_full_notm}} CLI" caption-side="top"}


For more information, see [{{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli).


## API methods
{: #settings-about-api}


The following table lists the actions that you can run to manage settings:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Get settings information   | `GET`            | `<ENDPOINT>/api/v3/settings`              |
| Update settings            | `PATCH`            | `<ENDPOINT>/api/v3/settings`  |
{: caption="Table 2. Settings actions by using the {{site.data.keyword.metrics_router_full_notm}} REST API" caption-side="top"}


For more information about the REST API, see [the settings API](https://{DomainName}/apidocs/metrics-router/metrics-router-v3#get-settings){: external}.
{: note}



### HTTP response codes
{: #settings-about-rc}


When you use the {{site.data.keyword.metrics_router_full_notm}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully.

- A 200 response always indicates success.
- A 4xx response indicates a failure.
- A 5xx response usually indicates an internal system error.

See the following table for some HTTP response codes:

| Status code | Status | Description |
|-------------|--------|-------------|
| `200` |	OK | The request was successful. |
| `201` |	OK | The request was successful. A resource is created. |
| `400` | Bad Request |	The request was unsuccessful. You might be missing a parameter that is required. |
| `401` |	Unauthorized | The IAM token that is used in the API request is invalid or expired. |
| `403` |	Forbidden | The operation is forbidden due to insufficient permissions. |
| `404` | Not Found |	The requested resource doesn't exist or is already deleted. |
| `429` |	Too Many Requests |	Too many requests hit the API too quickly. |
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.metrics_router_full_notm}} processing. |
{: caption="Table 3. List of HTTP response codes" caption-side="top"}
