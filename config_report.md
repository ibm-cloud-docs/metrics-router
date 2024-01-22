---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Creating a report of the {{site.data.keyword.metrics_router_full_notm}} configuration
{: #config_report}

After configuring your {{site.data.keyword.metrics_router_full}} resources for your account, you should save a copy of your configuration for reference and backup purposes.
{: shortdesc}

## Prereqs
{: #config_report_prereqs}

Before you use the CLI to save your {{site.data.keyword.metrics_router_full_notm}} resource data, you must do the following:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}} routes.](/docs/metrics-router?topic=metrics-router-iam)

4. Log in to {{site.data.keyword.cloud_notm}}. Run the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login).

5. Make sure you have configured your [settings](/docs/metrics-router?topic=metrics-router-settings), [targets](/docs/metrics-router?topic=metrics-router-target-manage&interface=cli) and [routes](/docs/metrics-router?topic=metrics-router-route_rules_definitions).


## Saving a copy of your account settings
{: #save_settings}

Run the following command to save a copy of your account settings to a file.

```text
ibmcloud metrics-router setting get --output JSON > ACCOUNT_settings.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.

## Saving a copy of your route configuration
{: #save_route}

Run the following command to save a copy of your route configuration to a file.

```text
ibmcloud metrics-router route ls --output JSON > ACCOUNT_routes.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.

## Saving a copy of your target configuration
{: #save_target}

Run the following command to save a copy of your target configuration to a file.

```text
ibmcloud metrics-router target ls --output JSON > ACCOUNT_targets.json
```
{: pre}

Where `ACCOUNT` is a unique indicator for your account.
