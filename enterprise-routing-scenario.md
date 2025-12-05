---

copyright:
  years:  2023, 2025
lastupdated: "2025-12-05"

keywords: enterprise

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Enterprise-managed routing
{: #enterprise-routing-scenario}


Use {{site.data.keyword.metrics_router_full}} to configure the routing of platform metrics from your enterprise child accounts to your enterprise parent account, then use {{site.data.keyword.iamshort}} (IAM) Action Control to restrict changes to the enterprise-managed routing.
{: shortdesc}

You can configure your enterprise child accounts to route all or a subset of platform metrics to an enterprise parent account. The child accounts contain Cloud resources that generate platform metrics. The parent account owns the enterprise and has {{site.data.keyword.mon_short}} instances that will contain the platform metrics from the child accounts.

The enterprise-managed routing configurations, from child accounts to parent account, can be locked by restricting the {{site.data.keyword.metrics_router_full}} enterprise actions with IAM Action Control. The child accounts can continue to manage their own account-managed {{site.data.keyword.metrics_router_full}} configurations, while the enterprise-managed configurations are restricted.

This example uses terraform automation to facilitate consistent routing configurations and Action Control restrictions across many child accounts. However, other configuration methods can be used as well.
{: tip}

![A diagram that shows a sample {{site.data.keyword.metrics_router_full}} enterprise configuration.](/images/metrics-router-enterprise-routing.svg "{{site.data.keyword.metrics_router_full}} enterprise configuration."){: caption="{{site.data.keyword.metrics_router_full}} enterprise configuration" caption-side="bottom"}

## Before you begin
{: #enterprise-routing-before-begin}

- To learn about how enterprise-manged IAM templates make your enterprise more secure, see [How enterprise-managed IAM access works](/docs/enterprise-management?topic=enterprise-management-access-enterprises&interface=ui#how-enterprise-iam).

- Be a member of the enterprise account to create and assign enterprise-managed IAM templates.

- To create, update, and delete an enterprise-managed IAM template, make sure that you are assigned with the following access:
   * A policy with the Template Administrator role on All IAM Account Management services.

- To assign an enterprise-managed IAM template to child accounts, make sure that you are assigned with the following access:
   * A policy with the Template Assignment Administrator role on All IAM Account Management services
   * A policy with at least the Viewer role on the Enterprise service.

- To create and assign action control templates, new and existing accounts in your enterprise must opt-in to enterprise-managed IAM. For more information, see [Opting in to enterprise-managed IAM](/docs/enterprise-management?topic=enterprise-management-enterprise-managed-opt-in).

- You must have Administrator role with permissions to manage {{site.data.keyword.metrics_router_full_notm}} in the source accounts. See [Managing access with IAM](/docs/metrics-router?topic=metrics-router-iam) and [Assigning access to {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-iam-assign-access).

## Step 1 - Create the parent account destination instance
{: #step-create-target-instance-terraform}
{: terraform}

Create the {{site.data.keyword.mon_full}} instance in the enterprise parent account. The instance will not receive platform metrics until the child accounts are configured.

```terraform
# NEW File: parent/main.tf

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

resource "ibm_resource_instance" "platform_monitoring_parent" {
  name              = "platform-monitoring-parent"
  service           = "sysdig-monitor"
  plan              = "graduated-tier"
  location          = "ca-tor"
  resource_group_id = data.ibm_resource_group.group.id

  parameters = {
    default_receiver = false
  }
}
```

This step creates an {{site.data.keyword.mon_full}} instance. The instance will not receive platform metrics until the child accounts are configured to send their platform metrics to the instance.


## Step 2 - Create parent authorization policies
{: #step-create-authorization-policy-terraform}
{: terraform}

Create an {{site.data.keyword.iamshort}} (IAM) service to service authorization policy in the parent account for each of your child accounts. In this example there are two child accounts.

```terraform
# FILE: parent/main.tf

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

locals {
  child_accounts = [
    "<INPUT_CHILD_A_ACCOUNT_ID>",
    "<INPUT_CHILD_B_ACCOUNT_ID>"
  ]
}

resource "ibm_iam_authorization_policy" "cross_account_policy" {
  for_each = toset(local.child_accounts)
  source_service_name         = "metrics-router"
  source_service_account      = each.key
  target_service_name         = "sysdig-monitor"
  target_resource_instance_id = ibm_resource_instance.platform_monitoring_parent.id
  roles                       = ["Supertenant Metrics Publisher"]
  description                 = "Authorize enterprise child account routing to the parent"
}
```
{: codeblock}

This step ensures {{site.data.keyword.metrics_router_full}} is authorized to route child A and child B account platform metrics to parent account.


## Step 3 - Create enterprise targets in child accounts
{: #step-create-child-enterprise-targets}
{: terraform}

Next, you need to create {{site.data.keyword.metrics_router_full}} enterprise targets in each child account, the target destination is the parent account's {{site.data.keyword.mon_short}} instance. In this example, there are only two child accounts, but there is no limitation to the number of child accounts that can be targeted to a single parent account.

Note the `managed_by = "enterprise"` parameter below.

```terraform
# NEW FILE: child_a/main.tf

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
  destination_crn = "<INPUT_PARENT_MONITORING_CRN>"
  name            = "child-a-target"
  managed_by      = "enterprise"
}
```
{: codeblock}

```terraform
# NEW FILE: child_b/main.tf

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
  destination_crn = "<INPUT_PARENT_MONITORING_CRN>"
  name            = "child-b-target"
  managed_by      = "enterprise"
}
```
{: codeblock}

This step creates {{site.data.keyword.metrics_router_full}} enterprise targets pointing to the parent {{site.data.keyword.mon_short}} instance. Routing is not yet enabled.

## Step 4 - Create enterprise routes in the child accounts
{: #step-create-child-enterprise-routes}
{: terraform}

Create {{site.data.keyword.metrics_router_full}} enterprise routes in each child account. You can route all platform metrics to the parent or a subset of platform metrics to the parent. In this example, child A and child B accounts will route all platform metrics to the parent.

See [IBM Cloud services that generate metrics that are managed through {{site.data.keyword.metrics_router_full}}](/docs/metrics-router?topic=metrics-router-cloud-services-mr).

```terraform
# FILE: child_a/main.tf

# Previous steps...

resource "ibm_metrics_router_route" "metrics_router_route" {
  lifecycle {
    create_before_destroy = true
  }
  name       = "child-a-route"
  managed_by = "enterprise"

  # Route all platform metrics to the hub.
  rules {
    action = "send"
    targets {
      id = ibm_metrics_router_target.metrics_router_target.id
    }
  }
}
```
{: codeblock}

```terraform
# FILE: child_b/main.tf

# Previous steps...

resource "ibm_metrics_router_route" "metrics_router_route" {
  lifecycle {
    create_before_destroy = true
  }
  name       = "child-b-route"
  managed_by = "enterprise"

  # Route all platform metrics to the hub.
  rules {
    action = "send"
    targets {
      id = ibm_metrics_router_target.metrics_router_target.id
    }
  }
}
```
{: codeblock}

This step creates the {{site.data.keyword.metrics_router_full}} enterprise routes. Platform metrics will be routed to the parent {{site.data.keyword.mon_short}} instance.


## Step 5 - Restrict enterprise actions with IAM Action Control
{: #step-restrict-enterprise-actions}
{: terraform}

Now that the enterprise-managed routing is created, you must restrict the usage of {{site.data.keyword.metrics_router_full}} enterprise actions so that the enterprise-managed routing cannot be modified by any entity. In this example, there is only one version of the action control template and it is assigned to each individual Account instead of the entire Enterprise or an Account Group.

In order to make changes to the enterprise-managed routing, you must delete the action control assignments.
{: note}

```terraform
# FILE: parent/main.tf

# Previous steps...

resource "ibm_iam_action_control_template" "metrics_router_enterprise_action_control_template" {
  name = "Metrics Router Enterprise Routing"
  description = "Restrict Metrics Router enterprise-managed routing"
  action_control {
    actions = [
      "metrics-router.enterprise-target.create",
      "metrics-router.enterprise-target.update",
      "metrics-router.enterprise-target.delete",
      "metrics-router.enterprise-route.create",
      "metrics-router.enterprise-route.update",
      "metrics-router.enterprise-route.delete"
    ]
    service_name = "metrics-router"
  }
  committed = "true"
}

locals {
  child_accounts = [
    "<INPUT_CHILD_A_ACCOUNT_ID>",
    "<INPUT_CHILD_B_ACCOUNT_ID>"
  ]
}

resource "ibm_iam_action_control_assignment" "metrics_router_enterprise_action_control_assignment" {
  for_each = toset(local.child_accounts)
  target = {
    type = "Account"
    id   = each.key
  }
  templates {
    id      = ibm_iam_action_control_template.metrics_router_enterprise_action_control_template.template_id
    version = ibm_iam_action_control_template.metrics_router_enterprise_action_control_template.version
  }
}
```
{: codeblock}

This step ensures {{site.data.keyword.metrics_router_full}} enterprise actions are restricted from further use, locking the enterprise-managed routing.


## Optional Step 6 - Account-managed routing
{: #step-account-managed-routing}
{: terraform}

Optionally, you can create account-managed routing in the enterprise child accounts or parent account; it will not conflict with the enterprise-managed routing created earlier. To create account-managed routing, ensure that the {{site.data.keyword.metrics_router_full}} target and route configurations have `managed_by = "account"`.
