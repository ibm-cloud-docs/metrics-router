---

copyright:
  years:  2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Reseting the permitted target regions in the account
{: #target-default-locations-reset}

To reset the {{site.data.keyword.metrics_router_full_notm}} account's permitted target regions, you must delete the permitted target regions from the account configuration.
{: shortdesc}


## Prereqs
{: #target-default-locations-reset-prereqs}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}} settings.](/docs/metrics-router?topic=metrics-router-iam)

4. Log in to {{site.data.keyword.cloud_notm}} by running the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Check your current account settings
{: #target-acct-reset-step1}
{: cli}
{: step}

To check your account's configuration and find out if there are default targets configured, run the following command:

```text
ibmcloud metrics-router setting get
```
{: pre}

The setting **Permitted target regions** lists the locations in the account that have been configured as valid locations where targets can be created.

## Reset the default targets
{: #target-acct-reset-step2}
{: cli}
{: step}

Run the following command to reset the account's default targets:

```sh
ibmcloud metrics-router setting update  --permitted-target-regions ""
```
{: pre}
