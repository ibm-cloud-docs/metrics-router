---

copyright:
  years:  2023, 2024
lastupdated: "2024-12-10"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}



# Understanding high availability and disaster recovery for {{site.data.keyword.metrics_router_full_notm}}
{: #metrics-router-ha-dr}

[High availability](#x2284708){: term} (HA) is the ability for a service to remain operational and accessible in the presence of unexpected failures. [Disaster recovery](#x2113280){: term} is the process of recovering the service instance to a working state.
{: shortdesc}

{{site.data.keyword.metrics_router_full}} is a highly available, multi-tenant, platform service. In this topic, you can learn more about {{site.data.keyword.metrics_router_full_notm}}'s availability strategy.

[High availability](#x2284708){: term} (HA) is a core discipline in an IT infrastructure to keep your apps up and running, even after a partial or full site failure. The main purpose of high availability is to eliminate potential points of failures in an IT infrastructure.


## Responsibilities
{: #ha_responsibilities}

For more information about your responsibilities when using {{site.data.keyword.metrics_router_full_notm}}, see [Shared responsibilities for {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-shared-responsibilities).



## Availability zones
{: #ha_locations}

{{site.data.keyword.metrics_router_full_notm}} is available in multiple regions. For more information on the regions where {{site.data.keyword.metrics_router_full_notm}} is available, see [Regions](/docs/metrics-router?topic=metrics-router-regions).

- Each region has three different data centers for redundancy configured in `active/active` mode.

- If all the data centers in a location fail, {{site.data.keyword.metrics_router_full_notm}} becomes unavailable in that location.

- In each supported region, traffic is load balanced across infrastructure in multiple availability zones, with no single point of failure.

For more information about service availability, see [Service Level Agreements (SLAs)](/docs/overview?topic=overview-slas).

The following table lists the high-availability (HA) status for the regions (locations) where the {{site.data.keyword.at_full_notm}} service is available:

| Geography             | Region                   | EU-Supported | HA Status |
|-----------------------|--------------------------|--------------|-----------|
| Asia Pacific        | Osaka (`jp-osa`)        | [Not applicable]{: tag-cool-gray}  | `MZR`     |
| Asia Pacific        | Sydney (`au-syd`)        | [Not applicable]{: tag-cool-gray}  | `MZR`     |
| Asia Pacific        | Tokyo (`jp-tok`)        | [Not applicable]{: tag-cool-gray}  | `MZR`     |
| Europe              | Frankfurt (`eu-de`)      | [Yes]{: tag-green}        | `MZR`     |
| Europe              | London (`eu-gb`)         | [Not applicable]{: tag-cool-gray}        | `MZR`     |
| Europe              | Madrid (`eu-es`)         | [Yes]{: tag-green}        | `MZR`     |
| North America       | Dallas (`us-south`)      | [Not applicable]{: tag-cool-gray}        | `MZR`     |
| North America       | Toronto (`ca-tor`)   | [Not applicable]{: tag-cool-gray}        | `MZR`     |
| North America       | Washington DC (`us-east`)   | [Not applicable]{: tag-cool-gray}        | `MZR`     |
| South America       | Sao Paulo (`br-sao`)   | [Not applicable]{: tag-cool-gray}        | `MZR`     |
{: caption="List of locations where the service is available." caption-side="top"}



Where
* A *geography* is a geographic area or larger political body that contains one or more regions.
* A *region* is a defined geographic territory.

    A region could be a specific postal code area, a town, a city, a state, a group of states, or even a group of countries.

    A region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

* `N/A` means feature that is not applicable to that geography.
* `MZR` means multi-zone region. [Learn more](/docs/overview?topic=overview-locations#table-mzr).


## Data availability
{: #ha_data_availability}

The data that is managed by {{site.data.keyword.metrics_router_full_notm}} in a region is kept in the data centers near that region.

A multizone region (MZR) consists of 3 or more availability zones that are independent from each other to ensure that single failure metrics affect only a single zone.

By default, {{site.data.keyword.metrics_router_full_notm}} is deployed across 3 zones. Each zone is set up with active/active/active:
* Each zone is located in a different data center in the region.
* The data in each zone is automatically replicated to the other zones with low latency. You don't need to do anything to enable the replication.
* The service is designed to withstand a single zone failure with no interruption.

The MZR architecture offers automatic failover between zones within the region, and high availability for an instance withing a region.

{{site.data.keyword.metrics_router_full_notm}} data includes information on where and how to collect and store metrics in your account.
- A target defines a resource where you can collect metrics.
- A route defines the rules that determine where metrics are routed in your account or cross-account.

{{site.data.keyword.metrics_router_full_notm}} does regular backups of the data per region:
- The settings metadata locations indicate the region where data is backup.
- Regular backups are done daily.
- {{site.data.keyword.metrics_router_full_notm}} data is replicated across regions based on your account configuration for the primary and backup metadata locations.

{{site.data.keyword.metrics_router_full_notm}} data is replicated across multiple regions.
- Regular backups are stored across multiple regions, and are restorable to other regions.

The following table shows the regions where the copy of a regular backup is replicated and available:

| Geography             | Region                   | Other regions that keep a copy of the backup   |
|-----------------------|--------------------------|-------------------------|
| Asia Pacific        | Osaka (`jp-osa`)        | Tokyo (`jp-tok`)     |
| Asia Pacific         | Sydney (`au-syd`)        | London (`eu-gb`)        |
| Asia Pacific        | Tokyo (`jp-tok`)        | Osaka (`jp-osa`)     |
| Europe               | Frankfurt (`eu-de`)      | Madrid (`eu-es`)        |
| Europe               | London (`eu-gb`)         | Sydney (`au-syd`)       |
| Europe               | Madrid (`eu-es`)         | Frankfurt (`eu-de`)     |
| North America        | Dallas (`us-south`)      | Washington (`us-east`)  |
| North America        | Toronto (`ca-tor`)       | Washington (`us-east`)  |
| North America        | Washington (`us-east`)   | Dallas (`us-south`)     |
| South America        | Sao Paulo (`br-sao`)     | Washington (`us-east`)  |
{: caption="List of locations where a copy of the backup is available" caption-side="top"}

## Disaster recovery strategy
{: #bc-dr-strategy}

{{site.data.keyword.cloud_notm}} has [business continuity](#x3026801){: term} plans in place to provide for the recovery of services within hours if a disaster occurs. You are responsible for your data backup and associated recovery of your content.

{{site.data.keyword.metrics_router_full_notm}} provides mechanisms to protect your data and restore service functions. Business continuity plans are in place to achieve targeted [recovery point objective](#x3429911){: term} (RPO) and [recovery time objective](#x3167918){: term} (RTO) for the service. The following table outlines the targets for {{site.data.keyword.metrics_router_full_notm}}.


| Recovery objective for DR                                         | Estimated time |
|-------------------------------------------------------------------|----------------|
| Maximum Tolerable Downtime (MTD) / Recovery Time Objective (RTO)  | Less than 24 hours |
| Recovery Point Objective (RPO)                                    | Less than 24 hours |
{: caption="RPO and RTO for IBM Cloud Metrics Routing" caption-side="bottom"}

## Locations
{: #bc-dr-locations}

For more information about service availability within regions and data centers, see [Service and infrastructure availability by location](/docs/overview?topic=overview-services_region).

The following table indicates the recovery region in the event of a DR situation:

| Geography             | Source region            | Recovery region   |
|-----------------------|--------------------------|--------------|
| Asia Pacific        | Osaka (`jp-osa`)        | Tokyo (`jp-tok`)     |
| Asia Pacific        | Sydney (`au-syd`)        | Frankfurt (`eu-de`)     |
| Asia Pacific        | Tokyo (`jp-tok`)        | Osaka (`jp-osa`)     |
| Europe              | Frankfurt (`eu-de`)      | Madrid (`eu-es`)        |
| Europe              | London (`eu-gb`)         | Frankfurt (`eu-de`)     |
| Europe              | Madrid (`eu-es`)         | Frankfurt (`eu-de`)     |
| North America       | Dallas (`us-south`)      | Washington (`us-east`)  |
| North America       | Toronto (`ca-tor`)       | Washington (`us-east`)  |
| North America       | Washington DC (`us-east`)   | Dallas (`us-south`)     |
| South America       | Sao Paulo (`br-sao`)     | Washington (`us-east`)     |
{: caption="List of locations where a region is recovered" caption-side="top"}





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
