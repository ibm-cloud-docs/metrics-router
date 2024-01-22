---

copyright:
  years:  2023, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Managing routes
{: #route-manage}

You can manage routes in your account by using the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and the {{site.data.keyword.metrics_router_full_notm}} Terraform provider. A route defines the rules that indicate what metrics are routed in a region and where to route them.
{: shortdesc}

For more information on {{site.data.keyword.metrics_router_full_notm}} routes, see [routes](/docs/metrics-router?topic=metrics-router-routes&interface=cli).



## About routes
{: #route-manage-about}

You can configure {{site.data.keyword.metrics_router_full_notm}} to route metrics that are generated in different regions where the service is supported to a target destination.

-  You can only route metrics that are generated in regions where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Regions](/docs/metrics-router?topic=metrics-router-regions).

- If you have regulatory and compliance requirements, check the route rules comply with them.



## IAM Access
{: #route-manage-iam}

You must have the correct IAM permissions to manage routes. For information, see [Managing IAM access.](/docs/metrics-router?topic=metrics-router-iam)


## CLI prerequisites
{: #route-manage-cli-prereqs}
{: cli}

Before you use the CLI to manage routes, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)


## Creating a route by using the CLI
{: #route-manage-cli-create}
{: cli}

Use this command to create a route.

Route names are unique in the account.
{: note}

```sh
ibmcloud metrics-router route create --name ROUTE_NAME ( --rules RULES |  --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #route-manage-cli-create-cmd}

`--name ROUTE_NAME`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--rules RULES`
:   JSON formatted rules array definition in single quotes that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).

`--file RULES_DEFINITION_JSON_FILE`
:    JSON file that includes the routing rules that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-manage-cli-create-sample}

The following is an example using the **`ibmcloud metrics-router route create`** command.

This example shows an example successful route creation.
{: note}

```text
ibmcloud mr route create --name target1 --rules '[{"action": "send", "targets":[{"id":"551957a7-c1e3-4160-84d8-4268709f6743"}]}]'
OK
Route
Name:         target1
ID:           06a29ca2-40f5-4371-ae3c-76a896577bd3
CRN:          crn:v1:bluemix:public:metrics-router:global:a/xxxx::route:06a29ca2-40f5-4371-ae3c-76a896577bd3
Rule 0:       [[551957a7-c1e3-4160-84d8-4268709f6743(mon-std)], []]
Created At:   2023-05-30T21:14:21.460Z
Updated At:   2023-05-30T21:14:21.460Z

```
{: screen}



## Updating a route using the CLI
{: #route-manage-cli-update}
{: cli}

Use this command to update a route. Any specified value that is different from when the route was originally created will be updated to the value specified in the command.

```sh
ibmcloud metrics-router route update --route ROUTE [--name ROUTE_NAME] ( --rules RULES |  --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #route-manage-cli-update-cmd}

`--route ROUTE`
:   The ID or current route name.

`--name route_NAME`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--rules RULES`
:   JSON formatted rules array definition in single quotes that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).

`--file RULES_DEFINITION_JSON_FILE`
:    JSON file that includes the routing rules that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-manage-cli-update-sample}

The following is an example using the **`ibmcloud metrics-router route update --route my-route --name my-new-route-name`** command.

```text
ibmcloud mr route update --route target1 --name target2
OK
Route
Name:         target2
ID:           06a29ca2-40f5-4371-ae3c-76a896577bd3
CRN:          crn:v1:bluemix:public:metrics-router:global:a/xxxx::route:06a29ca2-40f5-4371-ae3c-76a896577bd3
Rule 0:       [[551957a7-c1e3-4160-84d8-4268709f6743(mon-std)], []]
Created At:   2023-05-30T21:14:21.460Z
Updated At:   2023-05-30T21:19:40.953Z
```
{: screen}


## Deleting a route using the CLI
{: #route-manage-cli-delete}
{: cli}

Use this command to delete a route.

```sh
ibmcloud metrics-router ROUTE rm --route route [--force]
```
{: pre}

### Command options
{: #route-manage-cli-delete-cmd}

`--route ROUTE`
:   The ID or name of the route.

`--force` | `-f`
:   Will delete the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-manage-cli-delete-sample}

The following is an example using the **`ibmcloud metrics-router route rm --route xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`** command.

```text
Are you sure you want to remove the route with route ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx? [y/N]>y
OK
Route with name xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx was successfully removed.
```
{: screen}


## Getting information about a route using the CLI
{: #route-manage-cli-read}
{: cli}

Use this command to get information about a route for an {{site.data.keyword.metrics_router_full_notm}} region.

```sh
ibmcloud metrics-router ROUTE get --route route [--output FORMAT]
```
{: pre}

### Command options
{: #route-manage-cli-read-cmd}

`--route ROUTE`
:   The ID or name of the route.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format. If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-manage-cli-read-sample}

The following is an example using the **`ibmcloud metrics-router route get --route new-route-name`** command showing a route.

```text
ibmcloud mr route get --route route-all
OK
Route
Name:         route-all
ID:           f22e9cb6-2fcd-456d-9cf2-27813b1cc375
CRN:          crn:v1:bluemix:public:metrics-router:global:a/xxxx::route:f22e9cb6-2fcd-456d-9cf2-27813b1cc375
Rule 0:       [[551957a7-c1e3-4160-84d8-4268709f6743(mon-std)], []]
Created At:   2023-05-30T08:04:53.183Z
Updated At:   2023-05-30T08:53:22.824Z

```
{: screen}

## Listing all routes in a region
{: #route-manage-cli-list}
{: cli}

Use this command to list the configured routes for an {{site.data.keyword.metrics_router_full_notm}} region.

```sh
ibmcloud metrics-router route ls [--output FORMAT]
```
{: pre}

### Command options
{: #route-manage-cli-list-cmd}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #route-manage-cli-list-sample}

The following is an example using the **`ibmcloud metrics-router route ls`** command.

```text
ibmcloud mr route ls
OK
Routes
Name:         route-all
ID:           f22e9cb6-2fcd-456d-9cf2-27813b1cc375
CRN:          crn:v1:bluemix:public:metrics-router:global:a/xxxx::route:f22e9cb6-2fcd-456d-9cf2-27813b1cc375
Rule 0:       [[551957a7-c1e3-4160-84d8-4268709f6743(mon-std)], []]
Created At:   2023-05-30T08:04:53.183Z
Updated At:   2023-05-30T08:53:22.824Z
```
{: screen}


## API routes and actions
{: #route-manage-api-actions}
{: api}

The following table lists the actions that you can run to manage routes:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a route            | `POST`           | `<ENDPOINT>/api/v3/routes`              |
| Update a route            | `PATCH`            | `<ENDPOINT>/api/v3/routes/<route_ID>`  |
| Delete a route            | `DELETE`         | `<ENDPOINT>/api/v3/routes/<route_ID>`  |
| Read a route              | `GET`            | `<ENDPOINT>/api/v3/routes/<route_ID>`  |
| List all routes           | `GET`            | `<ENDPOINT>/api/v3/routes`             |
{: caption="Table 1. route actions by using the {{site.data.keyword.metrics_router_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage routes. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


* You can manage routes from the private network using an API endpoint with the following format: `https://private.REGION.metrics-router.cloud.ibm.com`
* You can manage routes from the public network using an API endpoint with the following format: `https://REGION.metrics-router.cloud.ibm.com`

* You can disable the public endpoints by updating the account settings. For more information, see [Configuring route and region settings](/docs/metrics-router?topic=metrics-router-settings).

For more information about the REST API, see [routes](https://{DomainName}/apidocs/metrics-router/metrics-router-v3#create-route){: external}.
{: note}


## API prerequisites
{: #route-manage-api-prereqs}
{: api}

To make API calls to manage routes, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/metrics-router?topic=metrics-router-iam-retrieve-token&interface=cli).
2. Identify the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).



## Creating a route using the API
{: #route-manage-api-create}
{: api}

You can use the following cURL command to create a route:

Route names are unique in the account. You cannot reuse a route name to configure multiple destinations.
{: note}

```shell
curl -X POST <ENDPOINT>/api/v3/routes -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    -d '{
    "name": "ROUTE_NAME",
    "rules": [
      RULES
    ]
  }'
```
{: codeblock}

Where

`<ENDPOINT>`
:   API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

`ROUTE_NAME`
:   The name to be given to the route.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`RULES`
:   JSON formatted rules array definition in single quotes that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).


For example, you can use the following cURL request to create a route:

```shell
curl -X POST https://private.us-south.metrics-router.cloud.ibm.com/api/v3/routes -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "My-route",
    "rules": [
      {
        "action": "send",
        "targets": [
          {
            "id": "50375218-7cff-4234-bbb4-171bebab8408"
          },
          {
            "id": "c7519d8a-5f97-498b-a229-8542f60955cd"
          }
        ],
        "inclusion_filters": [
          {
            "operand": "location",
            "operator": "is",
            "values": ["us-east"]
          },
          {
            "operand": "service_name",
            "operator": "in",
            "values": ["atracker","containers-registry"]
          }
        ]
      }
    ]
  }'
```
{: screen}


## Updating a route using the API
{: #route-manage-api-update}
{: api}

You can modify the name of a route and rules. Any specified value that is different from when the route was originally created will be updated to the value specified in the request.

When you update a route, you must include the route information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.

Route names are unique in the account. You cannot reuse a route name to configure multiple destinations.
{: note}

You can use the following cURL command to update a route:

```shell
curl -X PATCH <ENDPOINT>/api/v3/routes/ROUTE_ID -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "ROUTE_NAME",
    "rules": [
      RULES
    ]
  }'
```
{: codeblock}

Where

`<ENDPOINT>`
:   API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

`ROUTE_ID`
:   ID of the route.

`ROUTE_NAME`
:   Name of the route. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`RULES`
:   JSON formatted rules array definition in single quotes that define how metrics are routed. For more information, see [Defining routing rules](/docs/metrics-router?topic=metrics-router-route_rules_definitions).

For example, you can use the following cURL request to create a route in Dallas:

```shell
curl -X PATCH https://private.us-south.metrics-router.cloud.ibm.com/api/v3/routes -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "My route",
    "rules": [
      {
        "action": "send",
        "targets": [
          {
            "id": "50375218-7cff-4234-bbb4-171bebab8408"
          },
          {
            "id": "c7519d8a-5f97-498b-a229-8542f60955cd"
          }
        ],
        "inclusion_filters": [
          {
            "operand": "location",
            "operator": "is",
            "values": ["us-east"]
          },
          {
            "operand": "service_name",
            "operator": "in",
            "values": ["atracker","containers-registry"]
          }
        ]
      }
    ]
    }
  }'
```
{: screen}



## Deleting a route using the API
{: #route-manage-api-delete}
{: api}

You can use the following cURL command to delete a route:

```shell
curl -X DELETE <ENDPOINT>/api/v3/routes/<route_ID> -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

`<ENDPOINT>`
:   API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

`<route_ID>`
:   ID of the route.

For example, you can use the following cURL request to delete a route with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X DELETE https://private.us-south.metrics-router.cloud.ibm.com/api/v3/routes/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}


## Viewing a route using the API
{: #route-manage-api-read}
{: api}

You can use the following cURL command to view the configuration details of 1 route:

```shell
curl -X GET <ENDPOINT>/api/v3/routes/<route_ID> -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

`<ENDPOINT>`
:   API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).

`<route_ID>`
:   ID of the route.

For example, you can run the following cURL request to get information about a route with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X GET https://private.us-south.metrics-router.cloud.ibm.com/api/v3/routes/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}



## Listing all routes using the API
{: #route-manage-api-list}
{: api}

You can use the following cURL command to view all routes:

```shell
curl -X GET <ENDPOINT>/api/v3/routes -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a route. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


For example, you can run the following cURL request to get information about the routes that are defined in Dallas:

```shell
curl -X GET https://private.us-south.metrics-router.cloud.ibm.com/api/v3/routes -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}




## HTTP response codes
{: #route-manage-api-rc}
{: api}

When you use the {{site.data.keyword.metrics_router_full_notm}} REST API, you can get standard HTTP response codes to indicate whether a method completed successfully.

- A 200 response always indicates success.
- A 4xx response indicates a failure.
- A 5xx response indicates an internal system error.

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
{: caption="Table 2. List of HTTP response codes" caption-side="top"}
