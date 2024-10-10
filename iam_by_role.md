---

copyright:
  years:  2023, 2024
lastupdated: "2024-10-09"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}


# IAM actions by role
{: #iam_by_role}

The following tables show the {{site.data.keyword.metrics_router_full_notm}} actions by role.
{: shortdesc}

For {{site.data.keyword.metrics_router_full_notm}}, the IAM actions and Metrics Router actions are the same.
{: note}


## Operator
{: #iam_by_role_operator}


| Platform role | Metrics Router action | Action |
|---------------|-------------------------|-------------|
| Operator      | `metrics-router.target.read`  | View a target. |
| Operator      | `metrics-router.target.list`  | List all targets. |
| Operator      | `metrics-router.route.read`   | View a route. |
| Operator      | `metrics-router.route.list`   | List all routes. |
| Operator      | `metrics-router.setting.get`  | View configuration settings.  |
| Operator      | `metrics-router.onboarding.get` | For IBM use only. |
{: caption="{{site.data.keyword.metrics_router_full_notm}} actions for the operator role" caption-side="top"}


## Viewer
{: #iam_by_role_viewer}

| Platform role | Metrics Router action | Action |
|---------------|-------------------------|-------------|
| Viewer | `metrics-router.target.read` | View a target. |
| Viewer | `metrics-router.target.list` | List all targets. |
| Viewer | `metrics-router.route.read` | View a route. |
| Viewer | `metrics-router.route.list` | List all routes. |
| Viewer | `metrics-router.setting.get` | View configuration settings.  |
| Viewer      | `metrics-router.onboarding.get` | For IBM use only. |
{: caption="{{site.data.keyword.metrics_router_full_notm}} actions for the viewer role" caption-side="top"}

## Editor
{: #iam_by_role_editor}


| Platform role | Metrics Router action | Action |
|---------------|-------------------------|-------------|
| Editor | `metrics-router.target.read` | View a target. |
| Editor | `metrics-router.target.create` | Create a target. |
| Editor | `metrics-router.target.update` | Update a target. |
| Editor | `metrics-router.target.delete` | Delete a target. |
| Editor | `metrics-router.target.list` | List all targets. |
| Editor | `metrics-router.route.read` | View a route. |
| Editor | `metrics-router.route.create` | Create a route. |
| Editor | `metrics-router.route.update` | Update a route. |
| Editor | `metrics-router.route.delete` | Delete a route. |
| Editor | `metrics-router.route.list` | List all routes. |
| Editor | `metrics-router.setting.get` | View configuration settings.  |
| Editor | `metrics-router.onboarding.get` | For IBM use only. |
{: caption="{{site.data.keyword.metrics_router_full_notm}} actions for the editor role" caption-side="top"}


## Administrator
{: #iam_by_role_admin}

| Platform role | Metrics Router action | Action |
|---------------|-------------------------|-------------|
| Administrator | `metrics-router.target.read` | View a target. |
| Administrator | `metrics-router.target.create` | Create a target. |
| Administrator | `metrics-router.target.update` | Update a target. |
| Administrator | `metrics-router.target.delete` | Delete a target. |
| Administrator | `metrics-router.target.list` | List all targets. |
| Administrator | `metrics-router.route.read` | View a route. |
| Administrator | `metrics-router.route.create` | Create a route. |
| Administrator | `metrics-router.route.update` | Update a route. |
| Administrator | `metrics-router.route.delete` | Delete a route. |
| Administrator | `metrics-router.route.list` | List all routes. |
| Administrator | `metrics-router.setting.get` | View configuration settings.  |
| Administrator | `metrics-router.setting.update` | Update configuration settings. |
| Administrator | `metrics-router.onboarding.get` | For IBM use only. |
| Administrator | `metrics-router.onboarding.modify` | For IBM use only. |
| Administrator | `metrics-router.onboarding.delete` | For IBM use only. |
{: caption="{{site.data.keyword.metrics_router_full_notm}} actions for the administrator role" caption-side="top"}
