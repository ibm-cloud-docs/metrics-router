---

copyright:
  years:  2023, 2025
lastupdated: "2025-07-31"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.metrics_router_full_notm}}
{: #at_events}


{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.metrics_router_full}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.


## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}


{{site.data.keyword.metrics_router_full_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.




| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Montreal (`ca-mon`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|-------------------|----------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}



| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [Yes]{: tag-green} | [Yes]{: tag-green} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}


## Routing events using {{site.data.keyword.atracker_short}}
{: #at_events_ui_atracker}

{{site.data.keyword.atracker_short}} routes events based on the location that is specified in the `logSourceCRN` field included in the event.

You can define a target, the resource where events are routed to, in any {{site.data.keyword.atracker_short}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. For more information about supported targets, see [Targets](/docs/atracker?topic=atracker-atracker-resources#atracker-resources-targets).

You can define rules to determine where auditing events are to be routed by configuring 1 or more routes in the account. You can define rules for managing global events and location-based events that are generated in regions where {{site.data.keyword.atracker_short}} is supported. For more information, see [supported regions](/docs/atracker?topic=atracker-regions).

To view events, you must access the target and download the object.

## Viewing activity tracking events for {{site.data.keyword.metrics_router_full_notm}}
{: #at-viewing}

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #log-launch-standalone}

For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Management events
{: #at_events_mgt_atracker}

### Targets
{: #at_events_mgt_target}

The following table lists the auditing events that are generated when you manage targets:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `metrics-router.target.create`       | This event is generated when an administrator creates a new {{site.data.keyword.mon_short}} target.  |
| `metrics-router.target.list` | This event is generated when an administrator lists all targets defined under a region. |
| `metrics-router.target.read` | This event is generated when an administrator retrieves a target and its details by specifying the ID of the target.|
| `metrics-router.target.update` | This event is generated when an administrator updates a target details by specifying the ID of the target. |
| `metrics-router.target.delete` | This event is generated when an administrator deletes a target by specifying the ID of the target. |
{: caption="Events for managing targets" caption-side="top"}


### Routes
{: #at_events_mgt_route}

The following table lists the auditing events that are generated when you manage routes:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `metrics-router.route.create` | This event is generated when an administrator creates a route with rules that define how to route metrics data to targets. |
| `metrics-router.route.list` | This event is generated when an administrator lists routes.  |
| `metrics-router.route.read` | This event is generated when an administrator retrieves a route and its details by specifying the ID of the route. |
| `metrics-router.route.update` | This event is generated when an administrator replaces a route details by specifying the ID of the route. You can also get this event when you validate a target by checking the credentials to the destination target. |
| `metrics-router.route.delete` | This event is generated when an administrator deletes a route by specifying the ID of the route. |
{: caption="Events for managing routes" caption-side="top"}



### Settings
{: #at_events_setting}

The following table lists the auditing events that are generated when you manage settings:

| Action                                            | Description                |
|---------------------------------------------------|----------------------------|
| `metrics-router.setting.update` | This event is generated when an administrator configures the {{site.data.keyword.metrics_router_full_notm}} settings for an account. |
| `metrics-router.setting.get` | This event is generated when an administrator gets information about the {{site.data.keyword.metrics_router_full_notm}} settings for an account. |
{: caption="Events for managing settings" caption-side="top"}
