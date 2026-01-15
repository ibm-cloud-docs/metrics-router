---

copyright:
  years:  2023, 2026
lastupdated: "2026-01-14"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Managing {{site.data.keyword.mon_short}} targets
{: #target-manage}

You can manage {{site.data.keyword.mon_short}} targets in your account by using the {{site.data.keyword.metrics_router_full_notm}} UI, the {{site.data.keyword.metrics_router_full_notm}} CLI, the {{site.data.keyword.metrics_router_full_notm}} REST API, and the {{site.data.keyword.metrics_router_full_notm}} Terraform provider. A target is a resource where you can collect metrics.
{: shortdesc}

For more information on {{site.data.keyword.metrics_router_full_notm}} targets, see [Targets](/docs/metrics-router?topic=metrics-router-target).



## About {{site.data.keyword.mon_short}} targets
{: #target-manage-about}

You can configure {{site.data.keyword.metrics_router_full_notm}} to route metrics that are generated in different regions where the service is supported to a {{site.data.keyword.mon_short}} target.

-  You can only route metrics that are generated in regions where {{site.data.keyword.metrics_router_full_notm}} is available. For more information, see [Regions](/docs/metrics-router?topic=metrics-router-regions).

- If you have regulatory and compliance requirements, check the {{site.data.keyword.mon_short}} target is available in a valid location.

- To configure {{site.data.keyword.metrics_router_full_notm}} to route metrics to a {{site.data.keyword.mon_short}} instance, you must configure a service to service authorization. You do not have to provide credentials to {{site.data.keyword.metrics_router_full_notm}}. You can define a service to service authorization between the {{site.data.keyword.metrics_router_full_notm}} service and an instance of the {{site.data.keyword.mon_short}} service in the same account, or between the {{site.data.keyword.metrics_router_full_notm}} service and an instance of the {{site.data.keyword.mon_short}} service in a different account.

    For information on configuring Service to Service authentiation, see [Managing authorizations to grant access between services](/docs/metrics-router?topic=metrics-router-iam-service-auth).


## IAM Access
{: #target-manage-iam}

You must have the correct IAM permissions to manage targets. For information, see [Managing IAM access.](/docs/metrics-router?topic=metrics-router-iam)



## Creating a target using the UI
{: #target-create-ui}
{: ui}

Do the following to create a target using the UI.

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Monitoring**.

4. Click **Routing**.

5. Click the **Targets** tab.

6. Click **Create** to open the create panel.

7. **Service authorization required**: Service authorization is required to allow {{site.data.keyword.metrics_router_full_notm}} to communicate with {{site.data.keyword.mon_full_notm}}. Click **Authorize now** to create the policy automatically or click **Grant access in IAM**.

9.  **Choose destination**: Pick **Search by instance** or **Specify CRN**
    - **Search by instance**: Select an {{site.data.keyword.mon_full_notm}} instance from the table or click **Create** to create a new {{site.data.keyword.mon_full_notm}} instance.
    - **Specify CRN**: Enter the Cloud Resource Name (CRN) of the {{site.data.keyword.mon_full_notm}} instance. This enables you to enter a CRN from a different account.

10. Specify the target details.

    - **Target name**: Enter a meaningful name for the target.

    - **Target region**: Select the target region.

   - Toggle **Set as default target** to automatically set your new target as a default target in your {{site.data.keyword.metrics_router_full_notm}} settings. See the [default targets documentation](/docs/metrics-router?topic=metrics-router-planning&interface=ui#planning-4) for more details.

11. Click **Create target**.


## Updating a target using the UI
{: #target-update-ui}
{: ui}

Do the following to update a target using the UI.

Only resources in your account are listed and selectable. To specify a resource in a different account, select **Specify CRN** under **Choose destination**.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Monitoring**.

4. Click **Routing**.

5. Click the **Targets** tab.

6. Determine which target to update and click the ![Actions icon](../icons/action-menu-icon.svg "Actions").

7. Click **Unset as default** to remove your target as a default target in your {{site.data.keyword.metrics_router_full_notm}} settings. See [the default targets documentation](/docs/metrics-router?topic=metrics-router-planning&interface=cli#planning-4) for more details.

8. Click **Edit** to open the update panel.

9.  **Details**: Click **Edit** to update your target's name. You can also toggle **Default target** to add or remove your target as a default target in your {{site.data.keyword.metrics_router_full_notm}} settings.

    You can also view the routes associated with the target.
    {: tip}

10. Click **Save** to update your target.

11. **Destination**: Click **Edit** to change the {{site.data.keyword.mon_full_notm}} instance associated with your target.

12. Click **Save** to update your target.

## Deleting a target using the UI
{: #target-delete-ui}
{: ui}

Do the following to delete a target using the UI.

You cannot delete an {{site.data.keyword.metrics_router_full_notm}} target if it is used in a route or as a default target setting.
{: important}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Monitoring**.

4. Click **Routing**.

5. Click the **Targets** tab.

6. Determine which target to update and click the ![Actions icon](../icons/action-menu-icon.svg "Actions").

7. Click **Delete** and then click **Delete** in the confirmation panel.


## Listing all targets using the UI
{: #target-list-ui}
{: ui}

Do the following to list all the targets using the UI.

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.

2. Click the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg) &gt; **Observability**.

3. Click **Monitoring**.

4. Click **Routing**.

5. Click the **Targets** tab.

The table shows:

- Target type

- Destination name

- Destination region

- **Routes**: The number of routes if the target is used in any defined route.



## CLI prerequisites
{: #target-manage-cli-prereqs}
{: cli}

Before you use the CLI to manage targets, complete the following steps:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)

4. Before you configure {{site.data.keyword.metrics_router_full_notm}} routes or targets, you must configure a primary metadata region. The primary metadata region is configured using the [`ibmcloud metrics-router setting update` command `--primary-metadata-region` option.](/docs/metrics-router?topic=metrics-router-metrics-router-cli#settings-update-cli)


## Creating a {{site.data.keyword.mon_short}} target by using the CLI
{: #target-manage-cli-create}
{: cli}

Use this command to create a {{site.data.keyword.mon_short}} target to be used to configure a destination for platform metrics.

Target names are unique in the account.
{: note}

```sh
ibmcloud metrics-router target create --name TARGET_NAME --destination-crn CRN_VALUE [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-manage-cli-create-cmd}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region logged into, or targeted, will be used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--destination-crn CRN_VALUE`
:   The CRN of the {{site.data.keyword.mon_short}} instance.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-manage-cli-create-sample}

The following is an example using the **`ibmcloud metrics-router target create --name my-target --destination-crn crn:v1:bluemix:public:sysdig-monitor:au-syd:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::`** command.

This example shows an example successful target creation.
{: note}

```text
Target
Name:               		my-target
ID:                 		000000000-00000000-0000-0000-00000000
REGION:                         us-east
Type:               		sysdig_monitor
Destination CRN:     		crn:v1:bluemix:public:sysdig-monitor:au-syd:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
CreatedAt:            		2021-07-21T16:04:15.174Z
UpdatedAt:            		2021-07-21T16:04:15.174Z
```
{: screen}



## Updating a {{site.data.keyword.mon_short}} target using the CLI
{: #target-manage-cli-update}
{: cli}

Use this command to update a {{site.data.keyword.mon_short}} target. You can modify the name of a target and the destination CRN. Any specified value that is different from when the target was originally created will be updated to the value specified in the command.

Target names are unique in the account.
{: note}

```sh
ibmcloud metrics-router target update --target TARGET [--name TARGET_NAME] [--destination-crn DESTINATION_TARGET_CRN] [--output FORMAT]
```
{: pre}

### Command options
{: #target-manage-cli-update-cmd}

`--target TARGET`
:   The ID or current target name.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--destination-crn DESTINATION_TARGET_CRN`
:   The CRN of the {{site.data.keyword.mon_short}} instance.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-manage-cli-update-sample}

The following is an example using the **`ibmcloud metrics-router target update --target my-target --name my-new-target-name`** command.

```text
Target
Name:               		my-new-target-name
ID:                 		000000000-00000000-0000-0000-00000000
REGION:                         us-east
CRN:                		crn:v1:bluemix:public:metrics-router:us-south:a/xxxxxxxxxx:000000000-00000000-0000-0000-00000000
Type:               		sysdig_monitor
Destination CRN:     		crn:v1:bluemix:public:sysdig-monitor:au-syd:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
CreatedAt:            		2021-07-21T16:04:15.174Z
UpdatedAt:            		2021-07-21T16:04:15.174Z
```
{: screen}


## Deleting a target using the CLI
{: #target-manage-cli-delete}
{: cli}

Use this command to delete a target.

```sh
ibmcloud metrics-router target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-manage-cli-delete-cmd}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Will delete the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-manage-cli-delete-sample}

The following is an example using the **`ibmcloud metrics-router target rm --target xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`** command.

```text
Are you sure you want to remove the target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx? [y/N]>y
OK
Target with target ID xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx was successfully removed.
```
{: screen}


## Getting information about a target using the CLI
{: #target-manage-cli-read}
{: cli}

Use this command to get information about a target for an {{site.data.keyword.metrics_router_full_notm}} region.

```sh
ibmcloud metrics-router target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-manage-cli-read-cmd}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format. If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-manage-cli-read-sample}

The following is an example using the **`ibmcloud metrics-router target get --target new-target-name`** command showing a {{site.data.keyword.mon_short}} target.

```text
Name:               		my-target
ID:                 		000000000-00000000-0000-0000-00000000
REGION:                         us-east
CRN:                		crn:v1:bluemix:public:metrics-router:us-south:a/xxxxxxxxxx:000000000-00000000-0000-0000-00000000
Type:               		sysdig_monitor
Destination CRN:     		crn:v1:bluemix:public:sysdig-monitor:au-syd:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::
CreatedAt:            		2021-07-21T16:04:15.174Z
UpdatedAt:            		2021-07-21T16:04:15.174Z
```
{: screen}

## Listing all targets in a region
{: #target-manage-cli-list}
{: cli}

Use this command to list the configured targets for an {{site.data.keyword.metrics_router_full_notm}} region.

```sh
ibmcloud metrics-router target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-manage-cli-list-cmd}

`--output FORMAT`
:   Currently supported format is JSON. If specified, output will be returned in JSON format.  If `JSON` is not specified, output will be returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

### Example
{: #target-manage-cli-list-sample}

The following is an example using the **`ibmcloud metrics-router target ls`** command.

```text
Name                       ID                                     Region     Type              	CreatedAt                   UpdatedAt
target-01                  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx   us-south    sysdig_monitor    2020-11-18T03:52:08.603Z    2020-11-19T03:52:08.603Z
target-02                  yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy   us-south    sysdig_monitor    2020-11-18T03:52:01.592Z    2020-11-19T03:52:08.603Z
target-02-backup           zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz   us-east     sysdig_monitor    2021-02-26T06:53:13.466Z    2020-11-19T03:52:08.603Z
```
{: screen}


## API targets and actions
{: #target-manage-api-actions}
{: api}

The following table lists the actions that you can run to manage targets:

| Action                     | REST API Method  | API_URL                                          |
|----------------------------|------------------|--------------------------------------------------|
| Create a target            | `POST`           | `<ENDPOINT>/api/v3/targets`              |
| Update a target            | `PATCH`            | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| Delete a target            | `DELETE`         | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| Read a target              | `GET`            | `<ENDPOINT>/api/v3/targets/<TARGET_ID>`  |
| List all targets           | `GET`            | `<ENDPOINT>/api/v3/targets`             |
{: caption="Target actions by using the {{site.data.keyword.metrics_router_full_notm}} REST API" caption-side="top"}

You can use private and public endpoints to manage targets. For more information about the list of `ENDPOINTS` that are available, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


* You can manage targets from the private network using an API endpoint with the following format: `https://private.REGION.metrics-router.cloud.ibm.com`
* You can manage targets from the public network using an API endpoint with the following format: `https://REGION.metrics-router.cloud.ibm.com`

* You can disable the public endpoints by updating the account settings. For more information, see [Configuring target and region settings](/docs/metrics-router?topic=metrics-router-settings).

For more information about the REST API, see [Targets](https://{DomainName}/apidocs/metrics-router/metrics-router-v3#create-target){: external}.
{: note}


## API prerequisites
{: #target-manage-api-prereqs}
{: api}

To make API calls to manage targets, complete the following steps:
1. Get an IAM access token. For more information, see [Retrieving IAM access tokens](/docs/metrics-router?topic=metrics-router-iam-retrieve-token&interface=cli).
2. Identify the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).
3. Before you configure {{site.data.keyword.metrics_router_full_notm}} routes or targets, you must configure a primary metadata region. The primary metadata region is configured using the [modify settings API method.](/apidocs/metrics-router/metrics-router-v3#update-settings)



## Creating a {{site.data.keyword.mon_short}} target using the API
{: #target-manage-api-create}
{: api}

You can use the following cURL command to create a {{site.data.keyword.mon_short}} target:

Target names are unique in the account.
{: note}

```shell
curl -X POST <ENDPOINT>/api/v3/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "TARGET_NAME",
    "destination_crn": "CRN"
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.mon_short}} instance.


For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X POST https://private.us-south.metrics-router.cloud.ibm.com/api/v3/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "My-target",
    "target_type": "crn:v1:bluemix:public:sysdig-monitor:au-syd:a/xxxxxxxxxx:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxx::"
  }'
```
{: screen}

In the response, you get information about the target such as:
- The `id`, that indicates the GUID of the target
- The `crn`, that indicates the CRN of the target.
- The `write_status`, that indicates the status of the communication to the target destination. Use this information to debug problems with your target.


## Updating a {{site.data.keyword.mon_short}} target using the API
{: #target-manage-api-update}
{: api}

You can modify the name of a target and the destination CRN. Any specified value that is different from when the target was originally created will be updated to the value specified in the request.

When you update a {{site.data.keyword.mon_short}} target, you must include the target information in the data section of the request.
- You must pass all fields.
- Update the fields that need to be changed.

Target names are unique in the account.
{: note}

You can use the following cURL command to update a target:

```shell
curl -X PATCH <ENDPOINT>/api/v3/targets/TARGET_ID -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "TARGET_NAME",
    "destination_crn": "CRN"
  }'
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).
- `TARGET_ID` is the ID of the target.
- `TARGET_NAME` is the name of the target. The maximum length of the name is 256 characters.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

- `CRN` indicates the [CRN](/docs/account?topic=account-crn) of the {{site.data.keyword.mon_short}} instance.

For example, you can use the following cURL request to create a target in Dallas:

```shell
curl -X PATCH https://private.us-south.metrics-router.cloud.ibm.com/api/v3/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json" -d '{
    "name": "My target",
    "destination_crn": "crn:v1:bluemix:public:sysdig-monitor:au-syd:a/<account-id>:<instance-id>::"
    }
  }'
```
{: screen}



## Deleting a target using the API
{: #target-manage-api-delete}
{: api}

You can use the following cURL command to delete a target:

```shell
curl -X DELETE <ENDPOINT>/api/v3/targets/<TARGET_ID> -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).
- `<TARGET_ID>` is the ID of the target.


For example, you can use the following cURL request to delete a target with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X DELETE https://private.us-south.metrics-router.cloud.ibm.com/api/v3/targets/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}


## Viewing a target using the API
{: #target-manage-api-read}
{: api}

You can use the following cURL command to view the configuration details of 1 target:

```shell
curl -X GET <ENDPOINT>/api/v3/targets/<TARGET_ID> -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).
- `<TARGET_ID>` is the ID of the target.


For example, you can run the following cURL request to get information about a target with the ID `00000000-0000-0000-0000-000000000000`:

```shell
curl -X GET https://private.us-south.metrics-router.cloud.ibm.com/api/v3/targets/00000000-0000-0000-0000-000000000000 -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}



## Listing all targets using the API
{: #target-manage-api-list}
{: api}

You can use the following cURL command to view all targets:

```shell
curl -X GET <ENDPOINT>/api/v3/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: codeblock}

Where

- `<ENDPOINT>` is the API endpoint in the region where you plan to configure or manage a target. For more information, see [Endpoints](/docs/metrics-router?topic=metrics-router-endpoints).


For example, you can run the following cURL request to get information about the targets that are defined in Dallas:

```shell
curl -X GET https://private.us-south.metrics-router.cloud.ibm.com/api/v3/targets -H "Authorization: $ACCESS_TOKEN" -H "content-type: application/json"
```
{: screen}




## HTTP response codes
{: #target-manage-api-rc}
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
{: caption="List of HTTP response codes" caption-side="top"}
