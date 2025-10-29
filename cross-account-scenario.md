---

copyright:
  years:  2023, 2025
lastupdated: "2025-10-29"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Routing platform metrics across accounts
{: #cross-account-scenario}


Use {{site.data.keyword.metrics_router_full}} to configure the routing of platform metrics from multiple source accounts to a target account.
{: shortdesc}

You can configure your source accounts to route all or a subset of platform metrics to the target account. Source accounts are your accounts that contain Cloud resources that generate platform metrics regardless of the Cloud resource location. Target account refers to your account that contains the {{site.data.keyword.mon_short}} instance that will store the platform metrics.

This configuration implements a spoke–hub distribution system using the source account as the spoke and target account as the hub. Multiple spoke accounts send platform metrics to a centralized hub account simplifying observability across the multiple spoke accounts.

This example uses terraform. However, other configuration methods can be used as well.
{: tip}

![A diagram that shows a sample {{site.data.keyword.metrics_router_full_notm}} cross account configuration.](/images/metrics-router-cross-account.svg "{{site.data.keyword.metrics_router_full_notm}} cross account configuration."){: caption="{{site.data.keyword.metrics_router_full_notm}} cross account configuration" caption-side="bottom"}

## Prerequisites
{: #cross-account-prereqs}

- You must identify the hub account that you want to receive the platform metrics and the spoke accounts that will be sending the metrics to the hub account.

- You must have Administrator role with permissions to manage {{site.data.keyword.metrics_router_full_notm}} in the source accounts. See [Managing access with IAM](/docs/metrics-router?topic=metrics-router-iam) and [Assigning access to {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-iam-assign-access).

## Step 1 - Create the hub account instance
{: #step-create-target-instance-terraform}
{: terraform}

Create the {{site.data.keyword.mon_full}} instance to gain operational visibility into the performance and health of the applications, services, and platforms running on your spoke accounts.

```terraform
# NEW File: hub/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

data "ibm_resource_group" "group" {
  name = "Default"
}

resource "ibm_resource_instance" "platform_monitoring_hub" {
  name              = "platform-monitoring-hub"
  service           = "sysdig-monitor"
  plan              = "graduated-tier"
  location          = "ca-tor"
  resource_group_id = data.ibm_resource_group.group.id

  parameters = {
    default_receiver = false
  }
}
```

This step creates an {{site.data.keyword.mon_full}} instance. The instance will not receive platform metrics until the spoke accounts are configured to send their platform logs to the instance.


## Step 2 - Create hub authorization policies
{: #step-create-authorization-policy-terraform}
{: terraform}

Create an {{site.data.keyword.iamshort}} (IAM) service to service Authorization Policy in the hub account for each of your spoke accounts. In this example there are two spoke accounts.

```terraform
# FILE: hub/main.tf

# Previous steps...

locals {
  source_account_a = "<INPUT_SPOKE_A_ACCOUNT_ID>"
  source_account_b = "<INPUT_SPOKE_B_ACCOUNT_ID>"
}

resource "ibm_iam_authorization_policy" "hub_policy_source_a" {
  source_service_name         = "metrics-router"
  source_service_account      = local.source_account_a
  target_service_name         = "sysdig-monitor"
  target_resource_instance_id = ibm_resource_instance.platform_monitoring_hub.id
  roles                       = ["Supertenant Metrics Publisher"]
  description                 = "Authorize spoke A to hub"
}

resource "ibm_iam_authorization_policy" "hub_policy_source_b" {
  source_service_name         = "metrics-router"
  source_service_account      = local.source_account_b
  target_service_name         = "sysdig-monitor"
  target_resource_instance_id = ibm_resource_instance.platform_monitoring_hub.id
  roles                       = ["Supertenant Metrics Publisher"]
  description                 = "Authorize spoke B to hub"
}
```

This step ensures {{site.data.keyword.metrics_router_full}} is authorized to route spoke A and B account platform metrics to hub account.


## Step 3 - Create spoke targets
{: #step-create-spoke-targets}
{: terraform}

Now that the hub account is now fully configured, you need to create {{site.data.keyword.metrics_router_full_notm}} targets for each spoke account where the target destination is the hub account's {{site.data.keyword.mon_full}} instance. In this example, there are only two spoke accounts, but there is no limitation to the number of spoke accounts that can be targeted to a single hub account.

Accounts must set the Primary Metadata Region before creating targets or routes. See [Configuring account settings](/docs/metrics-router?topic=metrics-router-settings).
{: important}

```terraform
# NEW FILE: spoke_a/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

resource "ibm_metrics_router_settings" "metrics_router_settings" {
  primary_metadata_region = "<INPUT_METRICS_ROUTING_REGION>"
}

resource "ibm_metrics_router_target" "metrics_router_target" {
  destination_crn = "<INPUT_HUB_MONITORING_CRN>"
  name            = "spoke-a-target"
}
```

```terraform
# NEW FILE: spoke_b/main.tf

terraform {
  required_version = ">= 0.13"
  required_providers {
    ibm = {
      source  = "ibm-cloud/ibm"
      version = "~>1.81.0"
    }
  }
}

variable "ibmcloud_api_key" {
  description = "The IBM Cloud API key."
  type        = string
  sensitive   = true
}

provider "ibm" {
  ibmcloud_api_key = var.ibmcloud_api_key
}

resource "ibm_metrics_router_settings" "metrics_router_settings" {
  primary_metadata_region = "<INPUT_METRICS_ROUTING_REGION>"
}

resource "ibm_metrics_router_target" "metrics_router_target" {
  destination_crn = "<INPUT_HUB_MONITORING_CRN>"
  name            = "spoke-b-target"
}
```

This step creates {{site.data.keyword.metrics_router_full}} targets pointing to the hub {{site.data.keyword.mon_full}} instance; routing is not enabled yet.

## Step 4 - Create spoke routes
{: #step-create-spoke-routes}
{: terraform}

Create {{site.data.keyword.metrics_router_full_notm}} routes for each spoke account, you can route all platform metrics to the hub or a subset of platform metrics to the hub. In this example, spoke A will route all platform metrics to the hub and spoke B will route platform metrics from specific services and locations to the hub, explicitly discarding the rest.

See [IBM Cloud services that generate metrics that are managed through IBM Cloud Metrics Routing](/docs/metrics-router?topic=metrics-router-cloud-services-mr).

```terraform
# FILE: spoke_a/main.tf

# Previous steps...

resource "ibm_metrics_router_route" "metrics_router_route" {
  lifecycle {
    create_before_destroy = true
  }
  name = "spoke-a-route"

  # Route all platform metrics to the hub.
  rules {
    action = "send"
    targets {
      id = ibm_metrics_router_target.metrics_router_target.id
    }
  }
}
```

```terraform
# FILE: spoke_b/main.tf

# Previous steps...

resource "ibm_metrics_router_route" "metrics_router_route" {
  lifecycle {
    create_before_destroy = true
  }
  name = "spoke-b-route"

  # Route platform metrics for a few services, regardless of location, to the hub.
  rules {
    action = "send"
    targets {
      id = ibm_metrics_router_target.metrics_router_target.id
    }
    inclusion_filters {
      operand  = "service_name"
      operator = "in"
      values   = ["codeengine", "is", "metrics-router"]
    }
  }

  # Route platform metrics for one service and multiple locations to the hub.
  rules {
    action = "send"
    targets {
      id = ibm_metrics_router_target.metrics_router_target.id
    }
    inclusion_filters {
      operand  = "service_name"
      operator = "is"
      values   = ["atracker"]
    }
    inclusion_filters {
      operand  = "service_name"
      operator = "in"
      values   = ["ca-mon", "ca-tor"]
    }
  }

  # Drop and discard any other platform metric, hub receives nothing.
  rules {
    action = "drop"
  }
}
```

This step creates the {{site.data.keyword.metrics_router_full}} routes; platform metrics will route to the hub {{site.data.keyword.mon_full}} instance.


## Step 5 - Validate platform metrics
{: #step-validate-platform-metrics}
{: terraform}

Validate that the hub and spoke accounts are correctly configured.

1. [Launch the {{site.data.keyword.mon_full_notm}} UI](/docs/monitoring?topic=monitoring-launch) for the hub instance.
2. Look for **Dashboard Library > IBM** dashboard templates from the applicable Cloud services.
3. Use `ibm_scope` label to segment alerts and dashboards by spoke account.
