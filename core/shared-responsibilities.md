---

copyright:
  years:  2023, 2024
lastupdated: "2024-10-16"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# Understanding your responsibilities when using {{site.data.keyword.metrics_router_full_notm}}
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.metrics_router_full}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.metrics_router_full_notm}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview?topic=overview-terms).


## Incident and operations management
{: #incident-and-ops}

| Task              | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-------------------|-------------------------------------------------|-----------------------|
| Incident and operations management | Maintain service instances and infrastructure workloads. | Maintain incident and operations management of your data. |
| Monitor incidents  | Provide notifications for planned maintenance, security bulletins, or unplanned outages. | Set preferences to [receive emails about platform notifications](/docs/account?topic=account-email-prefs).   \n Monitor the [IBM Cloud announcements page](https://{DomainName}/status?selected=announcement) for general announcements. |
| Maintain {{site.data.keyword.cloud_notm}} high availability SLA for {{site.data.keyword.metrics_router_full_notm}}   | Provide {{site.data.keyword.metrics_router_full_notm}}  functionality across availability zones in a Multi-Zone Region (MZR).    \n Provide replication, fail-over features, and infrastructure maintenance and updates. | Keep your {{site.data.keyword.metrics_router_full_notm}}  configuration in a version control system so that you can reconfigure a region if needed.  \n  Comply with [Operational responsibilities when using {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-shared-responsibilities). |
| Monitor metrics for {{site.data.keyword.metrics_router_full_notm}}  | [Participating Cloud services](/docs/metrics-router?topic=metrics-router-cloud-services-mr) publish relevant data to their subscribing clients. Clients have the ability to receive this data once their account is configured. | [Configure your account](/docs/metrics-router?topic=metrics-router-getting-started) where Cloud service subscriptions publish metrics to receive the published metrics. Notice that {{site.data.keyword.metrics_router_full_notm}}  can only route metrics that are generated in [supported regions](/docs/metrics-router?topic=metrics-router-regions). Other regions, where {{site.data.keyword.metrics_router_full_notm}}  is not available, continue to manage events by using {{site.data.keyword.mon_short}} service. |
| Monitor {{site.data.keyword.metrics_router_full_notm}} targets  |  |  Check the health and status of the targets through {{site.data.keyword.mon_short}} by configuring alerts to notify of problems writing metrics to a target, and generate notifications, for example, to the {{site.data.keyword.mon_full_notm}} service. |
{: caption="Responsibilities for incident and operations" caption-side="top"}


## Change management
{: #change-management}

| Task                                                    | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|---------------------------------------------------------|-----------------------|--------|
| Updates to {{site.data.keyword.metrics_router_full_notm}} | Provide major, minor, and patch version updates for {{site.data.keyword.metrics_router_full_notm}} interfaces.   \n Document changes in the [IBM Cloud Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter) | `N/A` |
{: caption="Responsibilities for change management" caption-side="top"}



## Identity and access management
{: #iam-responsibilities}


| Task                           | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------|-------------------------------------------------|-----------------------|
| Manage permissions for {{site.data.keyword.metrics_router_full_notm}} | Provide the ability to restrict access to resources.   \n {{site.data.keyword.IBM_notm}} is responsible for the security and compliance of the {{site.data.keyword.metrics_router_full_notm}} feature. | Restrict access to {{site.data.keyword.metrics_router_full_notm}} by using Cloud IAM access policies. Define IAM policies to control which users within your account have access to manage the service and related resources in your account.    \n [Learn more about controlling access through IAM](/docs/metrics-router?topic=metrics-router-iam).|
| Configure authorization policies for each target | Support service to service authentication between {{site.data.keyword.metrics_router_full_notm}} and the {{site.data.keyword.mon_short}} service.   | [Configure 1 or more targets and corresponding authorization policies](/docs/metrics-router?topic=metrics-router-target-manage).  |
{: caption="Responsibilities for identity and access management" caption-side="top"}



## Security and regulation compliance
{: #security-compliance}


| Task                                       | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|--------------------------------------------|-------------------------------------------------|-----------------------|
| Meet security and compliance objectives  | Maintain controls that are commensurate to various industry compliance standards such as SOC2, PCI, HIPAA and Privacy Shield. For more information, see [Securing your data](/docs/metrics-router?topic=metrics-router-mng-data) | Set up and maintain security and regulation compliance for your apps and data.  |
{: caption="Responsibilities for security and regulation compliance" caption-side="top"}



## Disaster recovery
{: #disaster-recovery}


| Task                                                            | {{site.data.keyword.IBM_notm}} Responsibilities | Your Responsibilities |
|-----------------------------------------------------------------|-------------------------------------------------|-----------------------|
| Restore functionality for {{site.data.keyword.metrics_router_full_notm}}  | Automatically recover and restart {{site.data.keyword.metrics_router_full_notm}} components after any disaster event. | [Complete the disaster recovery (DR) steps for {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-bc-dr). |
| Backup {{site.data.keyword.metrics_router_full_notm}} components   | Daily backup of the {{site.data.keyword.metrics_router_full_notm}} infrastructure and components. | [Configure account settings](/docs/metrics-router?topic=metrics-router-settings), specifically, set up a primary metadata location and a backup metadata location. These locations keep information about the account routing rules and the target destination data to send data. Keep a copy of the setting configuration, definitions of targets, and definitions of routes in the account. For more information, see [Collecting information about resources](/docs/metrics-router?topic=metrics-router-config_report). |
{: caption="Responsibilities for disaster recovery" caption-side="top"}

`[*]` Recovered and restarted service components will not have customer data reloaded.
{: note}
