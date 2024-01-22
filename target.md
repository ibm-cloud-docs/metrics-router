---

copyright:
  years:  2023, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# About targets
{: #target}

You can manage {{site.data.keyword.metrics_router_full}} targets in your account by using the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and Terraform scripts. A target is a resource where you can collect metrics data. The resource can be located in the same {{site.data.keyword.cloud_notm}} account where metrics are generated or in a different account.
{: shortdesc}


## Understanding how targets work in your account
{: #target_behavior}

Note the following information about targets:

* Targets are regional under an account and can be accessed from any regional {{site.data.keyword.metrics_router_full_notm}} API endpoint.

* You can define a target in any of the supported locations where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Locations](/docs/metrics-router?topic=metrics-router-regions).

* You can configure up to 16 targets in each account.

* You can configure up to two default targets for each {{site.data.keyword.cloud_notm}} account.

    Default targets collect metrics from locations where you do not specify in the account where to route the metrics that are generated in that location.

* Information about targets is stored as metadata in the primary and backup locations that you set for the {{site.data.keyword.cloud_notm}} account. The information that is stored include details about the destinatiion resource and credentials to send metrics.

    The primary metadata location must be set prior to configuring a target.{: important}

    If you do not configure a primary metadata location, the location is set to the location where you define your first target in the account. For more information, see [Configuring account settings](/docs/metrics-router?topic=metrics-router-settings).

* You can use private and public endpoints to manage targets. For more information about the list of endpoints that are available, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

    * You can manage targets from the private network by using an API endpoint with the following format: `https://private.REGION.metrics-router.cloud.ibm.com`

    * You can manage targets from the public network by using an API endpoint with the following format: `https://REGION.metrics-router.cloud.ibm.com`

    * You can disable the public endpoints by updating the account settings. For more information, see [Enforcing private endpoints](/docs/metrics-router?topic=metrics-router-endpoints-enforce-private).

* The target name must be 1000 characters or less and cannot include any special characters other than space, dash `-`, dot `.`, underscore `_`, and colon `:`.

    The name must not include any personal identifying information (PII).
    {: important}


## Target types
{: #target_types}

You can configure any of the following target types:

| Target                                               | Type                     | Scope     | Description |
|------------------------------------------------------|--------------------------|-----------|------------|
| {{site.data.keyword.mon_full_notm}}                  | `sysdig-monitor`         | `Account` | Use this target to consolidate time series data to the region of your primary operations.  |
{: caption="Table 1. List of targets" caption-side="top"}


## IAM Access
{: #target_access}

To manage targets, ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-iam).

To allow the {{site.data.keyword.metrics_router_full_notm}} service to send metrics to your {{site.data.keyword.mon_short}} destinations, you must have a service to service authorization configured in the account where the target is located. For more information, see [Managing authorizations to grant access between services](/docs/metrics-router?topic=metrics-router-iam-service-auth).

## IAM permissions
{: #target_iam}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Task                    | IAM Action                     | IAM Policy scope  | IAM Roles          |
| ------------------------|--------------------------------|-------------------|----------------|
| Create a target         | `metrics-router.target.create` | Region            | `Administrator`  \n `Editor` |
| List all targets        | `metrics-router.target.list`   | Account           | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| Get details of a target | `metrics-router.target.read`   | Region            | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| Modify a target         | `metrics-router.target.update` | Region            | `Administrator`  \n `Editor` |
| Delete a target         | `metrics-router.target.delete` | Region            | `Administrator`  \n `Editor` |
{: caption="Table 2. IAM action scopes and roles for managing targets" caption-side="top"}

When you use the CLI, notice that you need the `metrics-router.target.list` role to create, read, update, or delete a target.
{: important}

## Auditing events
{: #target_at_events}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Task                    | Activity Tracker auditing event action    |
| ------------------------|-------------------------------------------|
| Create a target         | `metrics-router.target.create`            |
| List all targets        | `metrics-router.target.list`              |
| Get details of a target | `metrics-router.target.read`              |
| Modify a target         | `metrics-router.target.update`            |
| Delete a target         | `metrics-router.target.delete`            |
{: caption="Table 3. Activity Tracker auditing event action" caption-side="top"}


## CLI prerequisites
{: #target_v3_cli}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}}.](/docs/metrics-router?topic=metrics-router-iam)

2. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

3. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).


## CLI commands
{: #target_v3_cli_cmd}
{: cli}

The following table lists the actions that you can run to manage targets:

| Action                     | Command                             |
|----------------------------|-------------------------------------|
| `Create a target`            | `ibmcloud metrics-router target create`   |
| `Update a target`            | `ibmcloud metrics-router target update`   |
| `Delete a target`            | `ibmcloud metrics-router target rm`   |
| `Read a target`              | `ibmcloud metrics-router target get`      |
| `List all targets`           | `ibmcloud metrics-router target ls`       |
{: caption="Table 4. Target actions" caption-side="top"}


For more information, see [{{site.data.keyword.metrics_router_full_notm}} v3 CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli).

## API prerequisites
{: #target-prereqs-api}
{: api}

Before you use the API  to manage targets, complete the following steps:

1. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}}.](/docs/metrics-router?topic=metrics-router-iam)

2. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/metrics-router?topic=metrics-router-iam-retrieve-token&interface=cli).

3. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


## API methods
{: #target_v3_api}
{: api}

The following table lists the actions that you can run to manage targets:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| `Create a target`            | `POST`         | `<ENDPOINT>/api/v3/targets`              |
| `Update a target`            | `PATCH`        | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| `Delete a target`            | `DELETE`       | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| `Read a target`              | `GET`          | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| `List all targets`           | `GET`          | `<ENDPOINT>/api/v3/targets`             |
{: caption="Table 5. Target actions by using the {{site.data.keyword.metrics_router_full_notm}} REST API" caption-side="top"}


For more information, see [{{site.data.keyword.metrics_router_full_notm}} v3 API](https://{DomainName}/apidocs/metrics-router).


## HTTP response codes
{: #target_v3_api_rc}
{: api}

When you use the {{site.data.keyword.metrics_router_full_notm}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully.

- A 200 response always indicates success.
- A 4xx response indicates a failure.
- A 5xx response usually indicates an internal system error.

See the following table for some HTTP response codes:

| Status code | Status | Description |
|-------------|--------|-------------|
| `200` |	OK | The request was successful. |
| `201` |	OK | The request was successful. A resource is created. |
| `204` |	OK | The target was successfully deleted. |
| `400` | Bad Request |	The request was unsuccessful. You might be missing a parameter that is required. |
| `401` |	Unauthorized | The authorization request fails. |
| `403` |	Forbidden | The operation is forbidden due to insufficient permissions. |
| `404` | Not Found |	The requested resource doesn't exist or is already deleted. |
| `429` |	Too Many Requests |	Too many requests hit the API too quickly. |
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.metrics_router_full_notm}} processing. |
{: caption="Table 6. List of HTTP response codes" caption-side="top"}
