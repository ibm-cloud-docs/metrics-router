---

copyright:
  years:  2023, 2026
lastupdated: "2026-01-27"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# About routes
{: #routes}

You can manage routes in your account by using the {{site.data.keyword.metrics_router_full_notm}} UI, the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and the {{site.data.keyword.metrics_router_full_notm}} Terraform provider. A route defines the rules that indicate what metrics are routed in a region and where to route them.
{: shortdesc}


## Understanding how routes work in your account
{: #route_behaviour}

Note the following information about routes:

* Routes are global under an account and are evaluated in all regions where {{site.data.keyword.metrics_router_full}} is deployed.

* Routes may be accessed from any regional {{site.data.keyword.metrics_router_full_notm}} API endpoint.

* You can define up to 30 routes for an account.

* By default, the account has 0 routes configured.

* You can configure up to 10 rules for each route.

* You can configure up to 8 locations for each rule.

* You can configure up to 3 targets (`{ "targets": [{ "id": ID1 },{ "id": ID2 },{ "id": ID3 }] }`) for each rule.

* Routes are processed independently.  If you have multiple routes with rules that match the same metric data, that data will be sent to multiple targets.

* Rules in a single route definition are processed in order. The first matching rule (for example, `location`) that matches metrics data is used to process that data.  When metrics are processed, they will not be processed by a subsequent rule within that route's definition.

* Rules will match a metric if the metric's location is within a rule location. For example, rule location `eu-de` will match metric locations: `eu-de`, `eu-de-1`, `eu-de-2`, and `eu-de-3`. Or rule location `jp` will match all metrics within Japan. Run `ibmcloud catalog locations` to see the Cloud location hierarchies.

* If metrics data doesn't match any rule and no default target is configured, the metrics are dropped and not routed to any target.

* Any update to 1 or more rules in a route definition discards the existing rule set and replaces it with the specified configuration. When you update a route, you must define all existing rules in the rule set that do not change and add the changes to the rules that must be updated.

* Information about routes is stored as metadata in the primary location that you have set for the {{site.data.keyword.cloud_notm}} account.

    If you do not configure a primary metadata location, the location is set to the location where you define your first target in the account. For more information, see [Configuring account settings](/docs/metrics-router?topic=metrics-router-settings).

* You can use private and public endpoints to manage routes. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

    * You can manage routes from the private network by using an API endpoint with the following format: `https://private.REGION.metrics-router.cloud.ibm.com`

    * You can manage routes from the public network by using an API endpoint with the following format: `https://REGION.metrics-router.cloud.ibm.com`

    * You can disable the public endpoints by updating the account settings. For more information, see [Enforcing private endpoints](/docs/metrics-router?topic=metrics-router-endpoints-enforce-private).

* The route name must be 1000 characters or less and cannot include any special characters other than space, dash `-`, dot `.`, underscore `_`, and colon `:`.

    The name must not include any personal identifying information (PII).
    {: important}

After you configure a route, it might take up to 1 hour for the configuration to be enabled.
{: note}

## IAM Access
{: #route_access}

Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}}.](/docs/metrics-router?topic=metrics-router-iam)

## IAM permissions
{: #route_iam}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Task                    | IAM Action                     | IAM Policy scope  | IAM Roles          |
| ------------------------|--------------------------------|-------------------|----------------|
| Create a route         | `metrics-router.route.create` | Account            | `Administrator`  \n `Editor` |
| List all routes        | `metrics-router.route.list`   | Account           | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| Get details of a route | `metrics-router.route.read`   | Account            | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| Modify a route         | `metrics-router.route.update` | Account            | `Administrator`  \n `Editor` |
| Delete a route         | `metrics-router.route.delete` | Account            | `Administrator`  \n `Editor` |
{: caption="IAM action scopes and roles for managing routes" caption-side="top"}


## Auditing events
{: #route_at_events}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Task                    | Activity tracking auditing event action    |
| ------------------------|-------------------------------------------|
| Create a route         | `metrics-router.route.create`            |
| List all routes        | `metrics-router.route.list`              |
| Get details of a route | `metrics-router.route.read`              |
| Modify a route         | `metrics-router.route.update`            |
| Delete a route         | `metrics-router.route.delete`            |
{: caption="Activity tracking auditing event actions" caption-side="top"}



## CLI prerequisites
{: #route-prereqs-cli}
{: cli}

Before you use the CLI to manage routes, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).




## Managing routes using the UI
{: #route_ui}
{: ui}

You can manage your route definition using the {{site.data.keyword.metrics_router_full_notm}} UI. For more information, see [Managing routes](/docs/metrics-router?topic=metrics-router-route-manage&interface=ui).



## CLI commands
{: #route_v3_cli_cmd}
{: cli}

The following table lists the actions that you can run to manage routes:

| Action                     | Command                             |
|----------------------------|-------------------------------------|
| Create a route            | `ibmcloud metrics-router route create`   |
| Update a route            | `ibmcloud metrics-router route update`   |
| Delete a route            | `ibmcloud metrics-router route rm`   |
| Read a route              | `ibmcloud metrics-router route get`      |
| List all routes           | `ibmcloud metrics-router route ls`       |
{: caption="Route actions" caption-side="top"}


For more information, see [{{site.data.keyword.metrics_router_full_notm}} v3 CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli).

## API prerequsites
{: #route-prereqs-api}
{: api}

Before you use the API to manage routes, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/metrics-router?topic=metrics-router-iam-retrieve-token&interface=cli).
2. Identify the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


## API methods
{: #route-actions-api}
{: api}

The following table lists the actions that you can run to manage routes:

| Action                             | REST API Method  | API_URL                                          |
|------------------------------------|------------------|--------------------------------------------------|
| `Create a route`                     | `POST`           | `<ENDPOINT>/api/v3/routes`              |
| `Update a route`                     | `PATCH`            | `<ENDPOINT>/api/v3/routes/<ROUTE_ID>`  |
| `Delete a route`                     | `DELETE`         | `<ENDPOINT>/api/v3/routes/<ROUTE_ID>`  |
| `Get information about a route`      | `GET`            | `<ENDPOINT>/api/v3/routes/<ROUTE_ID>`  |
| `List all routes`                    | `GET`            | `<ENDPOINT>/api/v3/routes`             |
{: caption="Route actions by using the {{site.data.keyword.metrics_router_full_notm}} REST API" caption-side="top"}

For more information about the REST API, see [Routes](https://{DomainName}/apidocs/metrics-router/metrics-router-v3#create-route){: external}.
{: note}



## HTTP response codes
{: #route-target-rc}
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
| `204` |	OK | The route was successfully deleted. |
| `400` | Bad Request |	The request was unsuccessful. You might be missing a parameter that is required. |
| `401` |	Unauthorized | The IAM token that is used in the API request is invalid or expired. |
| `403` |	Forbidden | The operation is forbidden due to insufficient permissions. |
| `404` | Not Found |	The requested resource doesn't exist or is already deleted. |
| `429` |	Too Many Requests |	Too many requests reach the API too quickly. |
| `500` |	Internal Server Error |	Something went wrong in {{site.data.keyword.metrics_router_full_notm}} processing. |
{: caption="List of HTTP response codes" caption-side="top"}
