---

copyright:
  years:  2023, 2024
lastupdated: "2024-05-28"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Understanding business continuity and disaster recovery for {{site.data.keyword.metrics_router_full_notm}}
{: #bc-dr}

{{site.data.keyword.metrics_router_full}} is a highly available, multi-tenant, platform service. In this topic, you can learn more about {{site.data.keyword.metrics_router_full_notm}}'s disaster recovery strategy.
{: shortdesc}

[Disaster recovery](#x2113280){: term} involves a set of policies, tools, and procedures for returning a system, an application, or an entire data center to full operation after a catastrophic interruption. It includes procedures for copying and storing an installed system's essential data in a secure location, and for recovering that data to restore normalcy of operation.

## Responsibilities
{: #bc-dr-responsibilities}

For more information about your responsibilities when using {{site.data.keyword.metrics_router_full_notm}}, see [Shared responsibilities for {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-shared-responsibilities).

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

{{site.data.keyword.metrics_router_full_notm}} provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for {{site.data.keyword.metrics_router_full_notm}}.


| Recovery objective for DR                                         | Estimated time |
|-------------------------------------------------------------------|----------------|
| Maximum Tolerable Downtime (MTD) / Recovery Time Objective (RTO)  | Less than 24 hours |
| Recovery Point Objective (RPO)                                    | Less than 24 hours |
{: caption="Table 1. RPO and RTO for IBM Cloud Metrics Routing" caption-side="bottom"}

## Locations
{: #bc-dr-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

The following table indicates the recovery region in the event of a DR situation:

| Geography             | Source region            | Recovery region   |
|-----------------------|--------------------------|--------------|
| Asia Pacific        | Sydney (`au-syd`)        | Frankfurt (`eu-de`)     |
| Europe              | Frankfurt (`eu-de`)      | Madrid (`eu-es`)        |
| Europe              | London (`eu-gb`)         | Frankfurt (`eu-de`)     |
| Europe              | Madrid (`eu-es`)         | Frankfurt (`eu-de`)     |
| North America       | Dallas (`us-south`)      | Washington (`us-east`)  |
| North America       | Toronto (`ca-tor`)       | Washington (`us-east`)  |
| North America       | Washington DC (`us-east`)   | Dallas (`us-south`)     |
| South America       | Sao Paulo (`br-sao`)     | Washington (`us-east`)     |
{: caption="Table 2. List of locations where a region is recovered" caption-side="top"}





## Disaster recovery (DR) in a region
{: #bc-dr-cross-region-availability}

Disaster recovery is about surviving a catastrophic failure or loss of availability in one location.

{{site.data.keyword.metrics_router_full_notm}} is a platform service, there is no automatic cross-regional failover or cross-regional disaster recovery. If all of the availability zones in a region fail, {{site.data.keyword.metrics_router_full_notm}} becomes unavailable in that region.

[You can create a configuration to route to a backup target in a different region.](/docs/metrics-router?topic=metrics-router-dr_config)
{: tip}

In the event of a regional disaster, you must complete the following steps to establish cross-region high availability:

1. Decide which location is going to be your recovery region. Choose 1 of the following options:

    - [Check the suggested DR recovery region](/docs/metrics-router?topic=metrics-router-bc-dr#bc-dr-locations) and use that region as your recovery region.

    - If you have configured the {{site.data.keyword.metrics_router_full_notm}} account settings with a primary location and a secondary backup location, check if either location is still operational and use the one that is still operational as your recovery region.

    - If you have configured the {{site.data.keyword.metrics_router_full_notm}} account settings with a primary location only, and this location is down, check {{site.data.keyword.metrics_router_full_notm}} supported regions and choose an active region as your recovery region.

2. You can only define targets in {{site.data.keyword.metrics_router_full_notm}} supported regions. However, the actual target can be available in a different region and continue to be operational. First, you must check the target's availability. Next, choose 1 of the following options:

    - If a target is available in a different region from the one that is down, and the recovery region that you choose is one configured in the {{site.data.keyword.metrics_router_full_notm}} account settings, the primary location and backup secondary location include details of your target. You can continue to check the routes that are defined in the account to ensure that events are routed to the target.

    - If a target is available in a different region from the one that is down, and the recovery region that you choose is not a region that is configured in the {{site.data.keyword.metrics_router_full_notm}} account settings, you must configure the target in any {{site.data.keyword.metrics_router_full_notm}} supported region that is available, preferably, the region that you choose as your recovery region. Next, you must check the routes that are defined in the account so events are routed to the new target that you have configured.

    - If the target is not available, you must go through the DR recovery process of that type of target and provision a new one in the recovery region that you choose. You must configure the target in any {{site.data.keyword.metrics_router_full_notm}} supported region that is available, preferably, the region that you choose as your recovery region. Next, you must check the routes that are defined in the account so events are routed to the new target that you have configured.

3. You define routes to indicate how events are routed to the targets that you have configured in the account. These routes are global and not bound to a specific region. Therefore, in the case of a DR scenario, you must check that all the targets that are configured are operational, and that the rules apply to operational targets and locations.



When {{site.data.keyword.metrics_router_full_notm}} recovers in the region that is down, your configuration is restored. Complete the following steps to continue operating in the region that went down:
1. You must check that any existing targets in that region are also recovered and operational.
2. If you had configured new targets, you can update your configuration to go back to use the targets that went down. You can also decide to continue using the targets that you enabled in the recovery region.
