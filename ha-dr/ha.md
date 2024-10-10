---

copyright:
  years:  2023, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}



# Understanding high availability for {{site.data.keyword.metrics_router_full_notm}}
{: #ha}

{{site.data.keyword.metrics_router_full}} is a highly available, multi-tenant, platform service. In this topic, you can learn more about {{site.data.keyword.metrics_router_full_notm}}'s availability strategy.
{: shortdesc}

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
