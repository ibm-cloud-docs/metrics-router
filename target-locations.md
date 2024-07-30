---

copyright:
  years:  2023, 2024
lastupdated: "2024-07-30"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Enforcing target locations
{: #target-locations}

To enforce target locations in your {{site.data.keyword.cloud_notm}} account, you must configure {{site.data.keyword.metrics_router_full_notm}} account settings to limit the locations.
{: shortdesc}



## Prereqs
{: #target-locations-prereqs}
{: cli}

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. [Install the {{site.data.keyword.metrics_router_full_notm}} CLI](/docs/metrics-router?topic=metrics-router-metrics-router-cli-config).

3. Ensure you have the [correct IAM permissions to configure {{site.data.keyword.metrics_router_full_notm}} settings.](/docs/metrics-router?topic=metrics-router-iam)

4. Log in to {{site.data.keyword.cloud_notm}} by running the following command: [ibmcloud login](/docs/cli?topic=cli-ibmcloud_cli#ibmcloud_login)



## Step 1. Get details of your current account settings
{: #target-locations-step1}
{: cli}

Get details of your current account settings. Run the following command:

```text
ibmcloud metrics-router setting get
```
{: pre}

The setting **Permitted target regions** list all the locations where you allowed administrators to configure targets in the account.

## Step 2.
{: #target-locations-step2}
{: cli}

To manage the list of permitted regions, run the following command:

```text
ibmcloud metrics-router setting update --permitted-target-regions REGIONS
```
{: pre}

Where `REGIONS` define a comma-separated list of regions.

For example, you can run the following command to set 3 regions only:

```text
ibmcloud metrics-router setting update --permitted-target-regions "us-south","us-east","eu-de"
```
{: screen}
