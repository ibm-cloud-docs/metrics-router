---

copyright:
  years:  2023, 2024
lastupdated: "2024-08-15"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Enforcing default targets
{: #target-default}

You can configure up to two default targets for collecting metrics data that is not explicitly managed in the {{site.data.keyword.metrics_router_full_notm}} account's routing rules.
{: shortdesc}




## Managing default targets using the UI
{: #default_targets_ui}
{: ui}

You can manage your default targets using the {{site.data.keyword.metrics_router_full_notm}} UI. For more information, see [Creating a target using the UI](/docs/metrics-router?topic=metrics-router-target-manage&interface=ui#target-create-ui) and [Updating a target using the UI](/docs/metrics-router?topic=metrics-router-target-manage&interface=ui#target-update-ui).




## Prereqs
{: #target-default-prereqs}
{: cli}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}} settings.](/docs/metrics-router?topic=metrics-router-iam)

4. Log in to {{site.data.keyword.cloud_notm}} by running the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Identify targets
{: #target-default-step1}
{: cli}
{: step}

Get the list of targets that are defined in the account. Run the following command:

```text
ibmcloud metrics-router target ls
```
{: pre}

Copy the **ID** value of the targets that you want to configure in the account.

## Check your current account settings
{: #target-default-step2}
{: cli}
{: step}

To check your account's configuration and find out whether there are default targets that are configured, run the following command:

```text
ibmcloud metrics-router setting get
```
{: pre}

The **Default targets** setting lists any targets in the account that are configured as default targets.

## Configure default targets
{: #target-default-step3}
{: cli}
{: step}

Get the list of IDs for the targets that you want to configure as default targets. Then, run the following command to configure the default targets in the account:

When you run the command, make sure that you include the target IDs of all the default targets in the account. The command replaces the exiting configuration with the new one.
{: important}

```sh
ibmcloud metrics-router setting update --default-targets TARGETS
```
{: pre}

Where `TARGETS` represent the list of comma-separated target IDs.
