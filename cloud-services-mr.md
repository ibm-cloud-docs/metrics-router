---

copyright:
  years:  2023
lastupdated: "2023-06-06"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} services that generate metrics that are managed through {{site.data.keyword.metrics_router_full_notm}}
{: #cloud-services-mr}

List of {{site.data.keyword.cloud}} services that generate metrics that you can manage through {{site.data.keyword.metrics_router_full_notm}}.
{: shortdesc}

{{site.data.keyword.metrics_router_full_notm}} routes metrics based on the location, service-name, service-instance, resource, and resource-type that is specified in the CRN labels included with each metric. You can define a target, the resource where metrics are routed to, in any {{site.data.keyword.metrics_router_full_notm}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. You can define rules to determine where metrics are to be routed by configuring 1 or more routes in the account. You can define rules for managing routing of metrics that are generated in regions where {{site.data.keyword.metrics_router_full_notm}} is supported.
{: important}

## {{site.data.keyword.cloud_notm}} services
{: #cloud-services-mr-1}

| Service     | CRN service name |
|-------------|--------------|
| [{{site.data.keyword.appconfig_full}}](/docs/app-configuration?topic=app-configuration-getting-started) | `apprapp` |
|[{{site.data.keyword.codeenginefull}}](/docs/codeengine?topic=codeengine-getting-started) | `codeengine` |
| [{{site.data.keyword.registrylong}}](/docs/Registry?topic=Registry-getting-started) | `container-registry` |
| [{{site.data.keyword.dns_full}}](/docs/dns-svcs?topic=dns-svcs-getting-started) | `dns-svcs` |
| [{{site.data.keyword.en_full}}](/docs/event-notifications?topic=event-notifications-getting-started) | `event-notifications` |
| [{{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-operational-metrics) | `hs-crypto` |
| [Load Balancer for VPC](/docs/vpc?topic=vpc-load-balancers) | `is.load-balancer` |
| [{{site.data.keyword.messagehub_full}}](/docs/EventStreams?topic=EventStreams-getting_started) | `messagehub` |
| [MQ on IBM Cloud](/docs/mqcloud?topic=mqcloud-mqoc_getting_started) | `mqcloud` |
| [{{site.data.keyword.sqlquery_full}}](/docs/sql-query?topic=sql-query-overview#overview) | `sql-query` |
| [Toolchain](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd_about) | `toolchain` |
| [{{site.data.keyword.vmware-service_notm}}](/docs/vmwaresolutions) | `vmware` |
| [{{site.data.keyword.vmwaresolutions_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) | `vmware-solutions` |
{: caption="Table 1. {{site.data.keyword.cloud_notm}} services that send metrics to {{site.data.keyword.metrics_router_full_notm}}" caption-side="top"}


## {{site.data.keyword.cloud_notm}} platform services
{: #cloud-services-mr-2}


| Service     | CRN service name |
|-------------|--------------|
| [{{site.data.keyword.atracker_full_notm}}](/docs/atracker) | `atracker` |
| [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router) | `metrics-router` |
{: caption="Table 2. {{site.data.keyword.cloud_notm}} platform services that send metrics to {{site.data.keyword.metrics_router_full_notm}}" caption-side="top"}
