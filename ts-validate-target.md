---

copyright:
  years:  2022, 2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Incorrect or misconfigured target configuration
{: #ts-validate-target}
{: troubleshoot}
{: support}

The {{site.data.keyword.metrics_router_full_notm}} service cannot connect to a target and cannot route metrics to a destination target.
{: shortdesc}


Your dashboards display graphs with gaps due to missing metrics. You get an unauthorized RC 403 response when trying to access the target. A notification email is received indicating an incorrect target configuration.
{: tsSymptoms}


You can get this error in any of the following scenarios:
{: tsCauses}

- The CRN of the {{site.data.keyword.mon_short}} instance is not valid.
- The {{site.data.keyword.mon_short}} instance is deleted.
- The service to service authorization that is used by the {{site.data.keyword.metrics_router_full_notm}} service to authenticate with the {{site.data.keyword.mon_short}} instance is deleted or lack permissions.





To fix the configuration, complete the following tasks:
{: tsResolve}

- Check that the CRN of the {{site.data.keyword.mon_short}} instance matches the CRN that is configured in the target. For more information, see [Targets](/docs/metrics-router?topic=metrics-router-target-manage).
- Check that you have an authorization definition in **Manage** &gt; **Access (IAM)** &gt; **Manage access and users** &gt; **Authorization** for the {{site.data.keyword.metrics_router_full_notm}} service that allows you to authenticate with the {{site.data.keyword.mon_short}} instance whose connection is failing.
- Check the {{site.data.keyword.mon_short}} instance is available in the {{site.data.keyword.cloud_notm}} *Resources* dashboard.
