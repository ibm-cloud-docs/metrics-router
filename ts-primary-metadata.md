---

copyright:
  years:  2022, 2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Error when configuring a target or route
{: #ts-primary-metadata}
{: troubleshoot}
{: support}

You are trying to configure an {{site.data.keyword.metrics_router_full}} target or route and receive an error.
{: shortdesc}


When using the CLI or API you receive a message that the `metadata_primary_region` in settings is empty. API calls return a 409 error code.
{: tsSymptoms}


You must have a primary metadata region set before you can configure {{site.data.keyword.metrics_router_full_notm}} targets or routes.
{: tsCauses}


Configure your primary metadata region by using the [`ibmcloud metrics-router setting update` command](/docs/metrics-router?topic=metrics-router-metrics-router-cli#settings-update-cli) or the [modify settings API method.](/apidocs/metrics-router/metrics-router-v3#update-settings)
{: tsResolve}
