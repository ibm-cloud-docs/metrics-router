---

copyright:
  years:  2023, 2025
lastupdated: "2025-06-19"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} services that generate metrics that are managed through {{site.data.keyword.metrics_router_full_notm}}
{: #cloud-services-mr}

List of {{site.data.keyword.cloud}} services that generate metrics that you can manage through {{site.data.keyword.metrics_router_full_notm}}.
{: shortdesc}


There are 2 ways that services send metrics:
- As platform metrics

    You monitor these metrics through the monitoring instance that is configured to receive platform metrics. [Learn more about enabling platform metrics](/docs/monitoring?topic=monitoring-platform_metrics_enabling).

- By configuring a {{site.data.keyword.mon_short}} agent

    You configure the agent to send metrics to the {{site.data.keyword.mon_short}} instance that you choose. You monitor these metrics through that instance.


{{site.data.keyword.metrics_router_full_notm}} routes platform metrics based on the location, service-name, service-instance, resource, and resource-type that is specified in the CRN labels included with each metric. You can define a target, the resource where metrics are routed to, in any {{site.data.keyword.metrics_router_full_notm}} supported region. However, the target resource can be located in any region where that type of target is supported, in the same account or in a different account. You can define rules to determine where metrics are to be routed by configuring 1 or more routes in the account. You can define rules for managing routing of metrics that are generated in regions where {{site.data.keyword.metrics_router_full_notm}} is supported.
{: important}



## Container services
{: #container}

| Service     | CRN service name | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.registrylong_notm}}](/docs/Registry?topic=Registry-getting-started) |`container-registry` | [Platform metrics](/docs/Registry?topic=Registry-registry_monitor)|
{: caption="List of {{site.data.keyword.cloud_notm}} container services" caption-side="top"}


## Database services
{: #database}


| Service           |  CRN service name | Metrics |
|-------------------|-------------------|---------|
| [{{site.data.keyword.Db2_on_Cloud_short}}](/docs/Db2onCloud?topic=Db2onCloud-about)| `dashdb-for-transactions` | [Platform metrics](/docs/Db2onCloud?topic=Db2onCloud-monitor) |
| [{{site.data.keyword.databases-for-elasticsearch}}](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-getting-started&interface=ui) | `databases-for-elasticsearch` | [Platform metrics](/docs/databases-for-elasticsearch?topic=databases-for-elasticsearch-monitoring) |
| [{{site.data.keyword.databases-for-mongodb}}](/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started-new&interface=ui) | `databases-for-mongodb` | [Platform metrics](/docs/databases-for-mongodb?topic=databases-for-mongodb-monitoring) |
| [{{site.data.keyword.messages-for-rabbitmq}}](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-getting-started) | `messages-for-rabbitmq` | [Platform metrics](/docs/messages-for-rabbitmq?topic=messages-for-rabbitmq-monitoring) |
| [{{site.data.keyword.databases-for-postgresql}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started&interface=ui) | `databases-for-postgresql` | [Platform metrics](/docs/databases-for-postgresql?topic=databases-for-postgresql-monitoring) |
| [{{site.data.keyword.databases-for-enterprisedb}}](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-getting-started) [Deprecated]{: tag-deprecated} | `databases-for-enterprisedb` | [Platform metrics](/docs/databases-for-enterprisedb?topic=databases-for-enterprisedb-monitoring) |
| [{{site.data.keyword.databases-for-mysql}}](/docs/databases-for-mysql?topic=databases-for-mysql-getting-started&interface=cli) | `databases-for-mysql` | [Platform metrics](/docs/databases-for-mysql?topic=databases-for-mysql-monitoring) |
| [{{site.data.keyword.databases-for-redis}}](/docs/databases-for-redis?topic=databases-for-redis-getting-started&interface=ui) | `databases-for-redis` | [Platform metrics](/docs/databases-for-redis?topic=databases-for-redis-monitoring) |
| [{{site.data.keyword.databases-for-etcd}}](/docs/databases-for-etcd?topic=databases-for-etcd-getting-started) [Deprecated]{: tag-deprecated}  | `databases-for-etcd` | [Platform metrics](/docs/databases-for-etcd?topic=databases-for-etcd-monitoring) |
{: caption="List of database services" caption-side="top"}


## Storage services
{: #storage}

| Service           |  CRN service name | Metrics |
|-------------------|-------------------|---------|
| [{{site.data.keyword.cos_full}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage) | `cloud-object-storage` | [Platform metrics](/docs/cloud-object-storage?topic=cloud-object-storage-mm-cos-integration) |
{: caption="List of storage services" caption-side="top"}

## Developer tools
{: #devops}

The following table lists developer tools and DevOps services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | CRN service name | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.contdelivery_full}}](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started)| `toolchain` | [Platform metrics](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd-monitor-sysdig) |
| [{{site.data.keyword.appconfig_full}}](/docs/app-configuration?topic=app-configuration-getting-started)| `apprapp` | [Platform metrics](/docs/app-configuration?topic=app-configuration-ac-monitoring) |
| [{{site.data.keyword.en_full}}](/docs/event-notifications?topic=event-notifications-getting-started)|  `event-notifications` | [Platform metrics](/docs/event-notifications?topic=event-notifications-monitoring) |
| [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started) | `schematics` | [Platform metrics](/docs/schematics?topic=schematics-monitoring) |
{: caption="List of developer tools and DevOps services" caption-side="top"}


## Integration services
{: #integration}

The following table lists integration services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | CRN service name | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.messagehub}}](/docs/EventStreams?topic=EventStreams-getting-started)| `messagehub` | [Platform metrics](/docs/EventStreams?topic=EventStreams-metrics) |
| [{{site.data.keyword.mq_full}}](/docs/mqcloud?topic=mqcloud-getting_started)| `mqcloud` | [Platform metrics](/docs/mqcloud?topic=mqcloud-monitor_sysdig) |
{: caption="List of integration services" caption-side="top"}


## Networking services
{: #networking}

The following table lists services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | CRN service name | Metrics             |
|-------------|-------------|-------------------|
| [{{site.data.keyword.dns_full}}](/docs/dns-svcs?topic=dns-svcs-getting-started) | `dns-svcs` | [Platform metrics](/docs/dns-svcs?topic=dns-svcs-monitor-ibm-cloud-pm) |
| [{{site.data.keyword.loadbalancer_full}}](/docs/loadbalancer-service) | `ibm-cloud-load-balancer` | [Platform metrics](/docs/loadbalancer-service?topic=loadbalancer-service-monitoring-metrics) |
| [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) | `directlink` | [Platform metrics](/docs/dl?topic=dl-monitoring) |
| [{{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-getting-started) | `transit` | [Platform metrics](/docs/transit-gateway?topic=transit-gateway-monitoring) |
{: caption="List of networking services" caption-side="top"}


## {{site.data.keyword.cloud_notm}} platform services
{: #cloud-services-mr-2}

| Service     | CRN service name  | Metrics             |
|-------------|--------------|---------|
| [{{site.data.keyword.atracker_full_notm}}](/docs/atracker) | `atracker` |
| [{{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router) | `metrics-router` |
{: caption="{{site.data.keyword.cloud_notm}} platform services that send metrics to {{site.data.keyword.metrics_router_full_notm}}" caption-side="top"}


## Security services
{: #security}


| Service     | CRN service name | More info |
|-------------|-------------|-------------------------------------------------------------------------|
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started) | `hs-crypto` | [Platform metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics) |
| [{{site.data.keyword.keymanagementservicelong}}](/docs/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) | `kms` | [Platform metrics](/docs/key-protect?topic=key-protect-operational-metrics) |
| [{{site.data.keyword.secrets-manager_full}}](/docs/secrets-manager?topic=secrets-manager-getting-started) | `secrets-manager` | [Platform metrics](/docs/secrets-manager?topic=secrets-manager-operational-metrics) |
{: caption="List of security services" caption-side="top"}



## Serverless
{: #compute_serverless}


| Service     | CRN service name | Metrics |
|-------------|-------------|-------------------|
| [{{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-getting-started) | `codeengine` | [Platform metrics](/docs/codeengine?topic=codeengine-monitor)|
{: caption="List of serverless services" caption-side="top"}


## VMware
{: #vmware}

The following table lists Cloud services that are enabled for {{site.data.keyword.mon_full_notm}}:

| Service     | CRN service name | Metrics           |
|-------------|-------------|-------------------|
| [{{site.data.keyword.vmware-service_short}}](/docs/vmware-service?topic=vmware-service-getting-started) | `vmware` | [Platform metrics](/docs/vmware-service?topic=vmware-service-single-tenant-monitoring) |
| [VMware solutions](/docs/vmwaresolutions) | `vmware-solutions` | [Platform metrics](/docs/vmwaresolutions?topic=vmwaresolutions-shared-monitor) |
{: caption="VMware" caption-side="top"}



## VPC
{: #vpc}


| Service     | CRN service name | CRN resource type | Metrics    |
|-------------|-------------|-------------|-------------------|
| [VPC virtual server instances](/docs/vpc?topic=vpc-about-advanced-virtual-servers&interface=ui) | `is` | `[*]` | [Platform metrics](/docs/vpc?topic=vpc-vpc-monitoring-metrics)|
| [Flow Logs for VPC](/docs/vpc?topic=vpc-flow-logs) | `is` | `flow-log-collector` |  [Platform metrics](/docs/vpc?topic=vpc-fl-monitoring-metrics) |
| [Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers)| `is` | `load-balancer` | [Application Load Balancer platform metrics](/docs/vpc?topic=vpc-monitoring-metrics-alb) \n [Network Load Balancer platform metrics](/docs/vpc?topic=vpc-nlb_monitoring-metrics) |
| [VPN for VPC (site-to-site VPN)](/docs/vpc?topic=vpc-using-vpn)| `is.vpn` | `vpn` | [Platform metrics](/docs/vpc?topic=vpc-vpn-monitoring-metrics) |
| [Client VPN for VPC](/docs/vpc?topic=vpc-vpn-client-to-site-overview)| `is` | `vpn-server` | [Platform metrics](/docs/vpc?topic=vpc-vpn-client-to-site-monitoring) |
{: caption="List of VPC services (generation 2)" caption-side="top"}

`[*]` - VPC virtual server instances includes multiple CRN resource types.
 
In addition, some VPC resources have quotas associated with them that you can monitor through the VPC resource quota overview dashboard. For more information, see [VPC resource quota overview](/docs/vpc?topic=vpc-vpc-quota-metrics).


## Power IaaS services
{: #power_iaas}

| Service     | CRN service name | Metrics           |
|-------------|-------------|-------------------|
| [{{site.data.keyword.powerSys_notm}}](/docs/power-iaas?topic=power-iaas-getting-started) | `power-iaas` | [Platform metrics](/docs/power-iaas?topic=power-iaas-monitor-sysdig) |
{: caption="Power IaaS services" caption-side="top"}

## Watson AI services
{: #watson}

| Service     | CRN service name | Metrics           |
|-------------|-------------|-------------------|
| [{{site.data.keyword.lakehouse_short}}](/docs/watsonxdata) | `lakehouse` | [Platform metrics](/docs/watsonxdata?topic=watsonxdata-monitor_wxd) |
{: caption="Watson AI services" caption-side="top"}
