---

copyright:
  years: 2023, 2025
lastupdated: "2025-09-17"

subcollection: metrics-router

keywords:

---

{{site.data.keyword.attribute-definition-list}}

# Metrics Routing CLI
{: #metrics-router-cli}

The {{site.data.keyword.cloud}} command-line interface (CLI) provides extra capabilities for service offerings. This information describes how you can use the CLI to define and manage settings for your {{site.data.keyword.metrics_router_full}} instance by using the CLI.
{: shortdesc}

## Installing the CLI
{: #mr-cli-prereq}

* Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
* Install the CLI by running the following command:

   ```sh
   ibmcloud plugin install metrics-router
   ```
   {: pre}

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the most current commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

## Before you begin
{: #mr-prereq}

Before you configure {{site.data.keyword.metrics_router_full_notm}} routes or targets, you must configure a primary metadata region. The primary metadata region is configured using the [`ibmcloud metrics-router setting update` command `--primary-metadata-region` option.](#settings-update-cli)

If you you do not have a primary metadata region configured, your route and target command will fail.

## ibmcloud metrics-router route create
{: #route-create-cli}

Use this command to create a new route to {{site.data.keyword.metrics_router_full_notm}} targets.

Targets must be {{site.data.keyword.mon_full_notm}} instances.
{: restriction}

```sh
ibmcloud metrics-router route create --name ROUTE_NAME ( --rules RULES |  --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #route-create-options}

`--name ROUTE_NAME`
:   The name to be given to the route.

   Do not include any personal identifying information (PII) in any resource names.
   {: important}

`--file RULES_DEFINITION_JSON_FILE`
:   A JSON file that contains the definition of the rules for route. The file needs to be formatted as follows:

   ```json
   [
     {
       "targets": [{"id":"ID1"},{"id":"ID2"}]
     }
   ]
   ```
   {: codeblock}

   Where `targets` is a comma-separated list of target IDs.

   The rule definition can optionally also include inclusion filters. For example,

   ```json
   [{
       "action": "send",
       "targets": [{
         "id":"11111111-1111-1111-1111-111111111111"
       }],
       "inclusion_filters": [
           {
             "operand": "service_name",
             "operator": "in",
             "values": [
               "appconnect",
               "cloudant",
               "containers-kubernetes"
             ]
           },
           {
             "operand": "location",
             "operator": "in",
             "values": [
               "us-south",
               "eu-de"
             ]
           }
       ]
     }]
   ```
   {: codeblock}

    Where:

   `action`
   :   Action defines whether {{site.data.keyword.metrics_router_full}} includes or excludes metrics on the route. Two actions are supported: `send` and `drop`. If not specified, the default action is to send the metrics.

       `send`
       :   Metrics are sent, based on the routing rule, on the defined route.

       `drop`
       :   Metrics are excluded, based on the routing rule, when metrics are sent on the defined route.

   `operand`
   :   Operand is the name of the property on which the `operator` test is run. The following operands are supported: `location`,`service_name`,`service_instance`,`resource_type`, and `resource`.

   `operator`
   :   Two operators are supported: `in` and `is`.

       `in`
       :   The value of the operand property is compared to a list of values.

           You can define up to 20 values.

       `is`
       :   The value of the operand property is compared to a single value.

           When using `is`, only 1 value can be specified.

   `values`
   :   A string, or an array of strings, to be compared with the `operand` property to determine whether the metric is routed or not. When the `is` `operator` is used, `values` must include a single string. When the `in` `operator` is used, `values` can include multiple strings in an array.

       Valid values depend on the `operand`.

       `location`
       :   Any location where [{{site.data.keyword.metrics_router_full_notm}} is available.](/docs/metrics-router?topic=metrics-router-regions)

       `service_name`
       :   The CRN service name of an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

       `service_instance`, `resource_type`, and `resource`
       :   Values appropriate to an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotation marks. For example,

    ```json
    --rules '[{"action": "send", "targets":[{"id": "11111111-1111-1111-1111-111111111111"}], "inclusion_filters":[{"operand": "location","operator": "is","values": ["us-south"]}]}]
    ```
    {: codeblock}

    Where `targets` is a comma-separated list of target IDs.

    The rule definition can optionally also include inclusion filters. For example,

    ```json
    [{
        "action": "send",
        "targets": [{
          "id":"11111111-1111-1111-1111-111111111111"
        }],
        "inclusion_filters": [
            {
              "operand": "service_name",
              "operator": "in",
              "values": [
                "appconnect",
                "cloudant",
                "containers-kubernetes"
              ]
            },
            {
              "operand": "location",
              "operator": "in",
              "values": [
                "us-south",
                "eu-de"
              ]
            }
        ]
      }]
    ```
    {: codeblock}

    Where:

    `action`
    :   Action defines whether {{site.data.keyword.metrics_router_full}} includes or excludes metrics on the route. Two actions are supported: `send` and `drop`. If not specified, the default action is to send the metrics.

        `send`
        :   Metrics are sent, based on the routing rule, on the defined route.

        `drop`
        :   Metrics are excluded, based on the routing rule, when metrics are sent on the defined route.

    `operand`
    :   Operand is the name of the property on which the `operator` test is run. The following operands are supported: `location`,`service_name`,`service_instance`,`resource_type`, and `resource`.

    `operator`
    :   Two operators are supported: `in` and `is`.

        `in`
        :   The value of the operand property is compared to a list of values.

             You can define up to 20 values.

        `is`
        :   The value of the operand property is compared to a single value.

            When using `is`, only 1 value can be specified.

    `values`
    :   A string, or an array of strings, to be compared with the `operand` property to determine whether the metric is routed or not. When the `is` `operator` is used, `values` must include a single string. When the `in` `operator` is used, `values` can include multiple strings in an array.

        Valid values depend on the `operand`.

        `location`
        :   Any location where [{{site.data.keyword.metrics_router_full_notm}} is available.](/docs/metrics-router?topic=metrics-router-regions)

        `service_name`
        :   The CRN service name of an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

        `service_instance`, `resource_type`, and `resource`
        :   Values appropriate to an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

`--output FORMAT`
:   If `JSON` is specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`--force`
:   Run the command without prompting for confirmation. This flag only applies when the resulting route discards platform metrics.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router route update
{: #route-update-cli}

Use this command to update a route to {{site.data.keyword.metrics_router_full_notm}} targets. Any specified value that is different from when the route was originally created is updated to the value specified in the command.

Targets must be {{site.data.keyword.mon_full_notm}} instances.
{: restriction}

```sh
ibmcloud metrics-router route update --route ROUTE [--name ROUTE_NAME] ( --rules RULES |  --file RULES_DEFINITION_JSON_FILE ) [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #route-update-options}

`--route ROUTE`
:   The existing name or ID of the route.

`--name ROUTE_NAME`
:   The updated name to be given to the route (optional).

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--file RULES_DEFINITION_JSON_FILE`
:   A JSON file that contains the definition of the rules for route. The file needs to be formatted as follows:

    ```json
    [
      {
        "targets": [{"id":"ID1"},{"id":"ID2"}]
      }
    ]
    ```
    {: codeblock}

    Where `targets` is a comma-separated list of target IDs.

    The rule definition can optionally also include inclusion filters. For example,

    ```json
    [{
        "action": "send",
        "targets": [{
          "id":"11111111-1111-1111-1111-111111111111"
        }],
        "inclusion_filters": [
            {
              "operand": "service_name",
              "operator": "in",
              "values": [
                "appconnect",
                "cloudant",
                "containers-kubernetes"
              ]
            },
            {
              "operand": "location",
              "operator": "in",
              "values": [
                "us-south",
                "eu-de"
              ]
            }
        ]
      }]
    ```
    {: codeblock}

    Where:

    `action`
    :   Action defines whether {{site.data.keyword.metrics_router_full}} includes or excludes metrics on the route. Two actions are supported: `send` and `drop`. If not specified, the default action is to send the metrics.

        `send`
        :   Metrics are sent, based on the routing rule, on the defined route.

        `drop`
        :   Metrics are excluded, based on the routing rule, when metrics are sent on the defined route.

    `operand`
    :   Operand is the name of the property on which the `operator` test is run. The following operands are supported: `location`,`service_name`,`service_instance`,`resource_type`, and `resource`.

    `operator`
    :   Two operators are supported: `in` and `is`.

        `in`
        :   The value of the operand property is compared to a list of values.

            You can define up to 20 values.

        `is`
        :   The value of the operand property is compared to a single value.

            When using `is`, only 1 value can be specified.

    `values`
    :   A string, or an array of strings, to be compared with the `operand` property to determine whether the metric is routed or not. When the `is` `operator` is used, `values` must include a single string. When the `in` `operator` is used, `values` can include multiple strings in an array.

        Valid values depend on the `operand`.

        `location`
        :   Any location where [{{site.data.keyword.metrics_router_full_notm}} is available.](/docs/metrics-router?topic=metrics-router-regions)

        `service_name`
        :   The CRN service name of an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

        `service_instance`, `resource_type`, and `resource`
        :   Values appropriate to an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

`--rules RULES`
:   A JSON formatted rule definition enclosed in single quotation marks. For example,

    ```json
    --rules '[{"action": "send", "targets":[{"id": "11111111-1111-1111-1111-111111111111"}], "inclusion_filters":[{"operand": "location","operator": "is","values":["us-south"]}]}]
    ```
    {: codeblock}

    Where `target_ids` is a comma-separated list of target IDs.

    The rule definition can optionally also include inclusion filters. For example,

    ```json
    [{
        "action": "send",
        "targets": [{
          "id":"11111111-1111-1111-1111-111111111111"
        }],
        "inclusion_filters": [
            {
              "operand": "service_name",
              "operator": "in",
              "values": [
                "appconnect",
                "cloudant",
                "containers-kubernetes"
              ]
            },
            {
              "operand": "location",
              "operator": "in",
              "values": [
                "us-south",
                "eu-de"
              ]
            }
        ]
      }]
    ```
    {: codeblock}

    Where:

    `action`
    :   Action defines whether {{site.data.keyword.metrics_router_full}} includes or excludes metrics on the route. Two actions are supported: `send` and `drop`. If not specified, the default action is to send the metrics.

        `send`
        :   Metrics are sent, based on the routing rule, on the defined route.

        `drop`
        :   Metrics are excluded, based on the routing rule, when metrics are sent on the defined route.

    `operand`
    :   Operand is the name of the property on which the `operator` test is run. The following operands are supported: `location`,`service_name`,`service_instance`,`resource_type`, and `resource`.

    `operator`
    :   Two operators are supported: `in` and `is`.

        `in`
        :   The value of the operand property is compared to a list of values.

            You can define up to 20 values.

        `is`
        :   The value of the operand property is compared to a single value.

            When using `is`, only 1 value can be specified.

    `values`
    :   A string, or an array of strings, to be compared with the `operand` property to determine whether the metric is routed or not. When the `is` `operator` is used, `values` must include a single string. When the `in` `operator` is used, `values` can include multiple strings in an array.

        Valid values depend on the `operand`.

        `location`
        :   Any location where [{{site.data.keyword.metrics_router_full_notm}} is available.](/docs/metrics-router?topic=metrics-router-regions)

        `service_name`
        :   The CRN service name of an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

        `service_instance`, `resource_type`, and `resource`
        :   Values appropriate to an [{{site.data.keyword.cloud_notm}} service that generates metrics managed through [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr)

`--output FORMAT`
:   If `JSON` is specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`--force`
:   Run the command without prompting for confirmation. This flag only applies when the resulting route discards platform metrics.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router route rm
{: #route-rm-cli}

Use this command to delete an {{site.data.keyword.metrics_router_full_notm}} route.

```sh
ibmcloud metrics-router route rm --route ROUTE [--force]
```
{: pre}

### Command options
{: #route-rm-options}

`--route ROUTE`
:   The name or ID of the route to be deleted.

`--force`
:   Deletes the route without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router route get
{: #route-get-cli}

Use this command to get information about an {{site.data.keyword.metrics_router_full_notm}} route.

```sh
ibmcloud metrics-router route get --route ROUTE [--output FORMAT]
```
{: pre}

### Command options
{: #route-get-options}

`--route <ROUTE_ID>`
:   The name or ID of the route.

`--output FORMAT`
:   If `JSON` is specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router route ls
{: #route-ls-cli}

Use this command to list all the configured routes for {{site.data.keyword.metrics_router_full_notm}} in the account.

```sh
ibmcloud metrics-router route ls [--output FORMAT]
```
{: pre}

### Command options
{: #route-ls-options}

`--output FORMAT`
:   If `JSON` is specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router target create
{: #target-create-cli}

Use this command to create a target to be used to configure a destination for platform metrics.

Targets must be {{site.data.keyword.mon_full_notm}} instances.
{: restriction}

```sh
ibmcloud metrics-router target create --name TARGET_NAME --destination-crn DESTINATION_TARGET_CRN [--region REGION] [--output FORMAT]
```
{: pre}

### Command options
{: #target-create-options-at}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region that is logged into, or targeted, is used.

`--name TARGET_NAME`
:   The name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--destination-crn DESTINATION_TARGET_CRN`
:   The CRN of the service instance or resource to receive the metrics sent by {{site.data.keyword.metrics_router_full_notm}}. Ensure you have a service authorization between {{site.data.keyword.metrics_router_full_notm}} and your {{site.data.keyword.cloud_notm}} resource. For more information, see [Managing authorizations to grant access between services.](/docs/metrics-router?topic=metrics-router-iam-service-auth).

`--output FORMAT`
:   Support format is JSON. If specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router target update
{: #target-update-cli}

Use this command to update a target to be used to configure a destination for platform metrics.

Targets must be {{site.data.keyword.mon_full_notm}} instances.
{: restriction}

```sh
ibmcloud metrics-router target update --target TARGET [--name TARGET_NAME] [--destination-crn DESTINATION_TARGET_CRN] [--output FORMAT]
```
{: pre}

### Command options
{: #target-update-options}

`--region REGION` | `-r REGION`
:   Name of the region, for example, `us-south` or `eu-gb`. If not specified, the region that is logged into, or targeted, is used.

`--target TARGET`
:   The name or id of the target to be updated.

`--name TARGET_NAME`
:   The new name to be given to the target.

    Do not include any personal identifying information (PII) in any resource names.
    {: important}

`--destination-crn DESTINATION_TARGET_CRN`
:   The CRN of the service instance or resource to receive the metrics sent by {{site.data.keyword.metrics_router_full_notm}}. Ensure you have a service authorization between {{site.data.keyword.metrics_router_full_notm}} and your {{site.data.keyword.cloud_notm}} resource. For more information, see [Managing authorizations to grant access between services.](/docs/metrics-router?topic=metrics-router-iam-service-auth).

`--output FORMAT`
:   Support format is JSON. If specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router target rm
{: #target-delete-cli}

Use this command to delete a target.

```sh
ibmcloud metrics-router target rm --target TARGET [--force]
```
{: pre}

### Command options
{: #target-rm-options-cos}

`--target TARGET`
:   The ID or name of the target.

`--force` | `-f`
:   Deletes the target without providing the user with any additional prompt.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router target get
{: #target-get-cli}

Use this command to get information about an {{site.data.keyword.metrics_router_full_notm}} target.

```sh
ibmcloud metrics-router target get --target TARGET [--output FORMAT]
```
{: pre}

### Command options
{: #target-get-options}

`--target TARGET`
:   The ID or name of the target.

`--output FORMAT`
:   Supported format is JSON. If specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router target ls
{: #target-list-cli}

Use this command to list the configured targets for {{site.data.keyword.metrics_router_full_notm}}.

```sh
ibmcloud metrics-router target ls [--output FORMAT]
```
{: pre}

### Command options
{: #target-list-opts}

`--output FORMAT`
:   Supported format is JSON. If specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router setting get
{: #settings-get-cli}

Use this command to get the settings for the {{site.data.keyword.metrics_router_full_notm}} account configurations.

```sh
ibmcloud metrics-router setting get [--output FORMAT]
```
{: pre}

### Command options
{: #settings-get-options}

`--output FORMAT`
:   If `JSON` is specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

`help` | `--help` | `-h`
:   List options available for the command.

## ibmcloud metrics-router setting update
{: #settings-update-cli}

Use this command to modify current settings such as the default targets, permitted target regions, primary and secondary metadata regions in {{site.data.keyword.metrics_router_full_notm}}. Any value that is different from when the target was originally created is updated to the value specified in the command. If no options are specified, the current settings are returned.

Before you disable public endpoints by setting `--private-api-endpoint-only TRUE`, make sure your account has access to the private endpoint.  You can do this by running the command `ibmcloud account show`.  If `VRF Enabled` is `true` and `Service Endpoint Enabled` is `true` then you have access to the private endpoint. If you do not have access to the private endpoint, you cannot enable the public endpoint. Private endpoint access is required to enable the public endpoint.
{: important}

```text
ibmcloud metrics-router setting update [--primary-metadata-region REGION] [--backup-metadata-region REGION] [--private-api-endpoint-only ( TRUE | FALSE )] [--default-targets TARGET] [--permitted-target-regions REGIONS] [--output FORMAT] [--force]
```
{: pre}

### Command options
{: #settings-update-options}

`backup-metadata-region`
:   `backup-metadata-region` is the location where a backup of the metadata for your {{site.data.keyword.metrics_router_full_notm}} configuration is stored.

`default-targets`
:   `default-targets` is a list of target IDs. If no routing rules cause metrics to be sent to other targets, these targets receive the metrics. TARGET is a comma-separated list of target IDs.

`permitted-target-regions`
:   `permitted-target-regions` is the list of regions that can be used to define a target. REGION is a comma-separated list of regions. If not specified, any number of regions can be used to define a target.

    For example, to limit the regions that can be used to define targets to `us-south` and `eu-de`, specify: `--permitted-target-regions us-south,eu-de`.

    To delete all configured regions, specify `--permitted-target-regions ""`.

`primary-metadata-region`
:   `primary-metadata-region` is the location where the metadata for your {{site.data.keyword.metrics_router_full_notm}} configuration is stored.

`private-api-endpoint-only`
:   Specifies whether a private endpoint can be used. If `TRUE`, only a private endpoint can be used.

`--output FORMAT`
:   If `JSON` specified, output is returned in JSON format. If `JSON` is not specified, output is returned in a tabular format.

 `help` | `--help` | `-h`
:   List options available for the command.
