---

copyright:
  years:  2022, 2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}



# Configuring the CLI to manage the {{site.data.keyword.metrics_router_full_notm}} account configuration
{: #metrics-router-cli-config}

You must configure your local {{site.data.keyword.metrics_router_full_notm}} CLI so that you can manage the {{site.data.keyword.metrics_router_full_notm}} account configuration by using CLI commands.
{: shortdesc}


Complete the following steps to install the {{site.data.keyword.metrics_router_full_notm}} CLI:

1. [Install the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli).

2. Get the versions that are available for the `metrics-router` CLI plug-in. Run the following command:

    ```text
    ibmcloud plugin repo-plugins
    ```
    {: pre}

    For example, to get the versions of the {{site.data.keyword.metrics_router_full_notm}} CLI plug-in, run the following command:

    ```text
    ibmcloud plugin repo-plugins | grep metrics-router
    ```
    {: pre}

    The output of the command lists the versions that are available.

3. Install the CLI plugin in your local system. Run the following command:

    ```text
    ibmcloud plugin install metrics-router [-v VERSION]
    ```
    {: pre}

    Where `VERSION` is the value of a listed version that is available for the plug-in.


If you have the {{site.data.keyword.metrics_router_full_notm}} CLI plug-in in your local system and you want to update the version of the plug-in, run the following command: `ibmcloud plugin update metrics-router`.
{: tip}

If you want to delete the {{site.data.keyword.metrics_router_full_notm}} CLI plug-in from your local system, run the following command: `ibmcloud plugin delete metrics-router`.
{: tip}
