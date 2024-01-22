---

copyright:
  years:  2023, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for {{site.data.keyword.metrics_router_full_notm}}
{: #iam}

Access to {{site.data.keyword.metrics_router_full}} configuration resources for users and applications in your account is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). For example, every user that accesses the {{site.data.keyword.metrics_router_full_notm}} service in your account must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.metrics_router_full_notm}}.
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.metrics_router_full_notm}} as operations that are allowed to be performed on the service. Each IAM action is mapped to an IAM platform role that you can assign to a user.

{{site.data.keyword.metrics_router_full_notm}} is a platform service. Therefore, when you assign a policy to a user to work with {{site.data.keyword.metrics_router_full_notm}}, you are assigning IAM platform roles.
{: note}




## IAM actions
{: #iam-actions}

The {{site.data.keyword.metrics_router_full_notm}} service provides the following IAM actions:

### Targets
{: #iam-actions-target}

The following table lists the IAM actions that are generated when you manage targets:

| Action                             | Description                |
|------------------------------------|----------------------------|
| `metrics-router.target.create`     | Create a new {{site.data.keyword.mon_short}} target.  |
| `metrics-router.target.list`       | List all targets defined under a region. |
| `metrics-router.target.read`       | Retrieve a target and its details by specifying the ID of the target.|
| `metrics-router.target.update`     | Update a target details by specifying the ID of the target. |
| `metrics-router.target.delete`     | Delete a target by specifying the ID of the target. |
{: caption="Table 1. IAM actions for managing targets" caption-side="top"}


### Routes
{: #iam-actions-routes}

The following table lists the IAM actions that are generated when you manage routes:

| Action                           | Description                |
|----------------------------------|----------------------------|
| `metrics-router.route.create`    | Create a route with rules that define how to route metrics data to targets. |
| `metrics-router.route.list`      | List routes.  |
| `metrics-router.route.read`      | Retrieve a route and its details by specifying the ID of the route. |
| `metrics-router.route.update`    | Replace a route details by specifying the ID of the route. Validate a target by checking the credentials to the destination target. |
| `metrics-router.route.delete`    | Delete a route by specifying the ID of the route. |
{: caption="Table 2. IAM actions for managing routes" caption-side="top"}


### Settings
{: #iam-actions-settings}

The following table lists the IAM actions that are generated when you manage settings:

| Action                          | Description                |
|---------------------------------|----------------------------|
| `metrics-router.setting.update` | Configure the {{site.data.keyword.metrics_router_full_notm}} settings for an account. |
| `metrics-router.setting.get`    | Get information about the {{site.data.keyword.metrics_router_full_notm}} settings for an account. |
{: caption="Table 3. IAM actions for managing settings" caption-side="top"}

## IAM roles
{: #iam-roles}

The {{site.data.keyword.metrics_router_full_notm}} service provides the following IAM roles to control access to the service.

| Platform role            | Scope         | Description of actions |
|--------------------------|---------------|------------------------|
| Viewer                   | All resources | As a viewer, you can view {{site.data.keyword.metrics_router_full_notm}} configuration resources such as routes, targets, and the account configuration settings. |
| Operator                 | All resources | As an operator, you can view {{site.data.keyword.metrics_router_full_notm}} configuration resources such as routes, targets, and the account configuration settings. |
| Editor                   | All resources | As an editor, you can view, create, update, and delete {{site.data.keyword.metrics_router_full_notm}} resources such as routes and targets. You can also view the account configuration settings.|
| Administrator            | All resources | As an administrator, you can view, create, update, and delete {{site.data.keyword.metrics_router_full_notm}} resources. You can also assign access policies to manage {{site.data.keyword.metrics_router_full_notm}} resources to other users in the account. |
{: caption="Table 4. IAM platform roles" caption-side="bottom"}

When you define a policy, the *Resources* scope must be set to **All resources**. If this is not set, you will not be able to manage your {{site.data.keyword.metrics_router_full_notm}} instance and you will get a return code of `403`.
{: important}

If a specific role and its actions don't fit the use case that you're looking to address, you can [create a custom role](/docs/account?topic=account-custom-roles&interface=ui#custom-access-roles) and pick the actions to include.
{: tip}

### Targets
{: #iam-roles-target}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Action               | IAM Policy scope  | IAM Roles          |
| ------------------------ | ----------------- | -------------- |
| `metrics-router.target.create` | Region            | `Administrator`  \n `Editor` |
| `metrics-router.target.list`   | Account           | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| `metrics-router.target.read`   | Region            | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer` |
| `metrics-router.target.update` | Region            | `Administrator`  \n `Editor` |
| `metrics-router.target.delete` | Region            | `Administrator`  \n `Editor` |
{: caption="Table 5. IAM action scopes and roles for managing targets" caption-side="top"}

When you use the CLI, notice that you need the `metrics-router.target.list` role to create, read, update, or delete a target.
{: important}

### Routes
{: #iam-roles-routes}

The following table lists the IAM actions, their scope and the roles required to manage routes.

| Action                          | IAM Policy scope | IAM roles |
| ----------------------------- | -------------- | -------- |
| `metrics-router.route.read`   | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` |
| `metrics-router.route.create` | Account        | `Administrator`  \n `Editor` |
| `metrics-router.route.update` | Account        | `Administrator`  \n `Editor` |
| `metrics-router.route.delete` | Account        | `Administrator`  \n `Editor` | Delete a route. |
| `metrics-router.route.list`   | Account        | `Administrator`  \n `Editor`  \n `Viewer`  \n `Operator` |
{: caption="Table 6. IAM action scopes and roles for managing routes" caption-side="top"}

### Settings
{: #iam-roles-settings}

The following table lists the IAM actions, their scope and the roles required to manage settings.

| Action                          | IAM Policy scope | IAM roles |
| ------------------------- | -------------- | ---------------------- |
| `metrics_router.setting.get`    | Accoount      | `Administrator`  \n `Editor`  \n `Operator`  \n `Viewer`   |
| `metrics_router.setting.update` | Account       | `Administrator`|
{: caption="Table 7. IAM action scopes and roles for managing settings" caption-side="top"}



## Assigning access to {{site.data.keyword.metrics_router_full_notm}}
{: #iam-assign-access-how}

You can assign access to {{site.data.keyword.metrics_router_full_notm}} by using any of the following methods:

* Access policies per user

* Access groups

    Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access.

    An access group can be created to organize a set of users, service IDs, and trusted profiles into a single entity that makes it easy for you to assign access. You can assign a single policy to the group instead of assigning the same access multiple times for an individual user or service ID.For more information, see [Setting up access groups](/docs/account?topic=account-groups).

    To organize a set of users and service IDs into a single entity that makes it easy for you to manage IAM permissions, use access groups. You can assign a single policy to the group instead of assigning the same access multiple times per individual user or service ID.
    {: tip}

* Trusted profiles

    You can use trusted profiles to grant different {{site.data.keyword.cloud}} identities access to resources in your account. Automatically grant federated users access to your account with conditions based on SAML attributes from your corporate directory. Or, use trusted profiles to set up fine-grained authorization for applications that are running in compute resources. This way, you aren't required to create service IDs or API keys for the compute resources. You can also establish trust with {{site.data.keyword.cloud_notm}} services or service IDs in another account to grant cross-account access. For more information, see [Creating trusted profiles](/docs/account?topic=account-create-trusted-profile).

For more information, see [Assigning access to {{site.data.keyword.metrics_router_full_notm}}](/docs/metrics-router?topic=metrics-router-iam-assign-access).
