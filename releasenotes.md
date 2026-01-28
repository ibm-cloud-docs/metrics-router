---

copyright:
  years:  2023, 2026
lastupdated: "2026-01-27"

keywords:

subcollection: metrics-router

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.metrics_router_full_notm}}
{: #metrics-router-release-notes}

Use these release notes to learn about the latest updates to {{site.data.keyword.metrics_router_full}}.
{: shortdesc}

## 27 January 2026
{: #metrics-router-jan2726}

Route rules now support location hierarchies
:   {{site.data.keyword.metrics_router_full_notm}} route rules previously only matched exact platform metric locations. Moving forward, a rule will match a metric if the metric's location is within a rule location. For example, rule location `eu-de` will now match metric locations: `eu-de`, `eu-de-1`, `eu-de-2`, and `eu-de-3`. Or rule location `jp` will now match all metrics within Japan. Run `ibmcloud catalog locations` to see the Cloud location hierarchies.

## 31 July 2025
{: #metrics-router-jul3125}

Montreal support
:   The {{site.data.keyword.metrics_router_full_notm}} service is fully supported in the Montreal (`ca-mon`) region.

## 9 July 2025
{: #metrics-router-jul0925}

Updated Montreal considerations
:   As {{site.data.keyword.cloud_notm}} provides support for the Montreal (`ca-mon`) region, you need to understand how {{site.data.keyword.cloud_notm}} Observability services are made available and the actions you need to take to operate in Montreal.



## 15 August 2024
{: #metrics-router-aug1524}
{: release-note}

Configure {{site.data.keyword.metrics_router_full_notm}} using the IBM Console
:   {{site.data.keyword.metrics_router_full_notm}} provides a new user interface through the IBM Console where you can configure routes, targets, and settings. For more information, see [Getting account settings using the UI](/docs/metrics-router?topic=metrics-router-settings&interface=ui#settings-get-ui).



## 13 June 2024
{: #metrics-router-jun1324}
{: release-note}

{{site.data.keyword.metrics_router_full_notm}} is available in Osaka and Tokyo.
:   Osaka (jp-osa) and Tokyo (jp-tok) are now online regions for {{site.data.keyword.metrics_router_full_notm}}. {{site.data.keyword.metrics_router_full_notm}} can be configured and endpoints can now be used in these regions.

## 10 June 2024
{: #metrics-router-jun1024}
{: release-note}

{{site.data.keyword.metrics_router_full_notm}} is available in Sao Paulo and Toronto.
:   Sao Paulo (br-sao) and Toronto (ca-tor) are now online regions for {{site.data.keyword.metrics_router_full_notm}}. {{site.data.keyword.metrics_router_full_notm}} can be configured and endpoints can now be used in these regions.

## 3 May 2024
{: #metrics-router-may0324}
{: release-note}

{{site.data.keyword.metrics_router_full_notm}} is planned to be supported in the br-sao, ca-tor, jp-osa, and jp-tok regions in June 2024.
:   You might need to consider changes to your {{site.data.keyword.metrics_router_full_notm}} configuration. For more information, see [Required actions for newly supported regions](/docs/metrics-router?topic=metrics-router-new_region_support&interface=cli).

## 10 April 2024
{: #metrics-router-apr1024}
{: release-note}

Increase routes and rules limits
:   The maximum number of routes for each account is increased to 30 and the maximum number of rules for each route is increased to 10.

## 26 September 2023
{: #metrics-router-sep2623}
{: release-note}

Madrid region support
:   Madrid is now an online region for {{site.data.keyword.metrics_router_full_notm}}. Services can now be provisioned in Madrid and Madrid endpoints can be used. Platform metrics will continue flowing to the Frankfurt region.


## 6 June 2023
{: #metrics-router-Jun0623}
{: release-note}

General availability of {{site.data.keyword.metrics_router_full_notm}}
:   [Learn more about {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router).
