---

copyright:
  years:  2023, 2024
lastupdated: "2024-09-25"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}

# Managing authorizations to grant access between services
{: #iam-service-auth}

Use {{site.data.keyword.cloud}} Identity and Access Management (IAM) to create or remove an authorization that grants {{site.data.keyword.metrics_router_full_notm}} access to the {{site.data.keyword.mon_full_notm}} service.
{: shortdesc}

Many of the capabilities of IAM are focused on managing and enforcing user and application access to {{site.data.keyword.cloud_notm}} resources. However, you might encounter other scenarios in which you need to provide one service with access to a user's resource in another service. This type of access is called an authorization.

In an authorization, the source service is the service that is granted access to the target service. The roles that you select define the level of access for the source service. The target service is the service that you are granting permission to be accessed by the source service based on the roles that you assign. A source service can be in the same account where the authorization is created or in another account. The target service is always in the account where the authorization is created. You can view whether the source service is located in the current account or another account by viewing the Source account column for the specific authorization on the [Authorizations](/iam/authorizations) page in the {{site.data.keyword.cloud_notm}} console.



## Permissions to manage authorizations
{: #iam-service-auth-permissions}

You must have access to the target service to manage authorization between services.

The autorization that you define for the {{site.data.keyword.metrics_router_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.mon_full_notm}} service.
{: important}



The following table outlines the permissions that are needed on the target service to be able to define an authorization:

| Action              | Administrator | Operator | Editor | Viewer |
|---------------------|---------------|----------|--------|--------|
| View all authorizations that are configured in the account | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | | | |
| Create authorizations | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | | | |
| Delete authorizations | ![Checkmark icon](../icons/checkmark-icon.svg "checkmark") | | | |
{: caption="Table 1. Actions on the target service that are required to manage authorizations" caption-side="top"}

Users can only see authorizations that they configure in the account.

## Creating an authorization in the console
{: #iam-service-auth-create-ui}
{: ui}

Complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** > **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source account.

    If the source service that needs access to the target service is in this account, select **This account**.

    If the source service that needs access to the target service is in a different account, select **Other account**. Then, enter the account ID of the source account.

4. Select {{site.data.keyword.metrics_router_full_notm}} as the source service. Then, set the scope of the access to **All resources**.

5. Select {{site.data.keyword.mon_full_notm}} as the target service. Then, set the scope of the access to **All resources** or a single instance by configuring **Resources based on selected attributes** &gt; **Service Instance**.

    Other attributes are not supported for this type of authorization.

6. In the *Service Access* section, select **Supertenant Metrics Publisher** to assign access to the source service that accesses the target service.

7. Click **Authorize**.

If you create an authorization between a service in another account and a target service in your current account, you need to have access only to the target resource. For the source account, you need only the account number. 
{: note}

## Creating an authorization by using the CLI
{: #iam-service-auth-create-cli}
{: cli}


You must have access to the target service to create an authorization between services. The authorization that you define for the {{site.data.keyword.metrics_router_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.mon_full_notm}} service.
{: important}

If you have the IAM permission to create policies and authorizations, you can grant only the level of access that you have as a user of the target service. For example, if you have viewer access for the target service, you can assign only the viewer role for the authorization. If you attempt to assign a higher permission such as administrator, it might appear that permission is granted, however, only the highest level permission you have for the target service, that is viewer, will be assigned. 
{: important}


Run the following command to create an authorization for the {{site.data.keyword.metrics_router_full_notm}} service.

```sh
ibmcloud iam authorization-policy-create metrics-router sysdig-monitor "Supertenant Metrics Publisher"
```
{: codeblock}

1. You can scope a specific IBM Cloud Monitoring instance using `[--target-service-instance-name TARGET_SERVICE_INSTANCE_NAME | --target-service-instance-id TARGET_SERVICE_INSTANCE_ID]`.
1. Do not provide any other scope options.

For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-create](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_create).


## Creating an authorization by using Terraform
{: #iam-service-auth-create-terra}
{: terraform}


Before you can create an authorization by using Terraform, make sure that you have completed the following:

- Install the Terraform CLI and configure the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform. For more information, see the tutorial for [Getting started with Terraform on {{site.data.keyword.cloud}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the {{site.data.keyword.cloud_notm}} APIs that are used to complete this task.
- Create a Terraform configuration file that is named `main.tf`. In this file, you define resources by using HashiCorp Configuration Language. For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

Use the following steps to create an authorization by using Terraform:

1. Create an authorization policy between services by using the `ibm_iam_authorization_policy` resource argument in your `main.tf` file.

   The following example creates an authorization between services:
   ```terraform
   resource "ibm_iam_authorization_policy" "policy" {
     source_service_name = "metrics-router"
     target_service_name = "sysdig-monitor"
     roles               = ["Supertenant Metrics Publisher"]
     description         = "Authorization Policy"
     transaction_id     = "terraformAuthorizationPolicy"
   }
   ```
   {: codeblock}

   The `ibm_iam_authorization_policy` resource requires the source service, target service, and role. The source service is granted access to the target service, and the role is the level of permission that the access allows. Optionally, you can add a description for the authorization and a transaction ID.
   {: note}

   - You may provide `target_resource_instance_id` to scope a specific IBM Cloud Monitoring instance.
   - For more examples, see the [Terraform documentation for authorization resources](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/iam_authorization_policy){: external}.

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initializing Working Directories](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Provisioning Infrastructure with Terraform](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

## Creating an authorization by using the API
{: #iam-service-auth-create-api}
{: api}

You must have access to the target service to create an authorization between services. You can grant only the level of access that you have as a user of the target service. The autorization that you define for the {{site.data.keyword.metrics_router_full_notm}} service requires that you have `Administrator` role for the {{site.data.keyword.mon_full_notm}} service.
{: important}

To authorize a source service access to a target service, use the [IAM Policy Management API](/apidocs/iam-policy-management#create-policy). See the following API example for Create a policy method with the `type=authorization` specified.

The supported attributes for creating an authorization policy depend on what each service supports. For more information about the supported attributes for each service, see the documentation for the services that you're using.
{: note}

```bash
curl --request POST \
  --url https://iam.cloud.ibm.com/v1/policies \
  --header 'Authorization: Bearer <token>' \
  --header 'Content-Type: application/json' \
  --data '{
    "type": "authorization",
    "subjects": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "<account-id>"
                },
                {
                    "name": "serviceName",
                    "value": "metrics-router"
                }
            ]
        }
    ],
    "roles": [
        {
            "role_id": "crn:v1:bluemix:public:sysdig-monitor::::serviceRole:Publisher"
        }
    ],
    "resources": [
        {
            "attributes": [
                {
                    "name": "accountId",
                    "value": "<account-id>"
                },
                {
                    "name": "serviceName",
                    "value": "sysdig-monitor"
                }
            ]
        }
    ]
}'
```
{: curl}
{: codeblock}

```java
SubjectAttribute accountSubjectAttribute = new SubjectAttribute.Builder()
      .name("accountId")
      .value(exampleAccountId)
      .build();

SubjectAttribute serviceNameSubjectAttribute = new SubjectAttribute.Builder()
      .name("serviceName")
      .value("metrics-router")
      .build();

PolicySubject policySubjects = new PolicySubject.Builder()
      .addAttributes(accountSubjectAttribute)
      .addAttributes(serviceNameSubjectAttribute)
      .build();

PolicyRole policyRoles = new PolicyRole.Builder()
      .roleId("crn:v1:bluemix:public:sysdig-monitor::::serviceRole:Publisher")
      .build();

ResourceAttribute accountIdResourceAttribute = new ResourceAttribute.Builder()
      .name("accountId")
      .value(exampleAccountId)
      .operator("stringEquals")
      .build();

ResourceAttribute serviceNameResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceName")
      .value("sysdig-monitor")
      .operator("stringEquals")
      .build();

ResourceAttribute serviceInstanceResourceAttribute = new ResourceAttribute.Builder()
      .name("serviceInstance")
      .value(exampleTargetInstanceId)
      .operator("stringEquals")
      .build();

ResourceAttribute resourceTypeResourceAttribute = new ResourceAttribute.Builder()
      .name("resourceType")
      .value(exampleResourceType)
      .operator("stringEquals")
      .build();

ResourceAttribute resourceResourceAttribute = new ResourceAttribute.Builder()
      .name("resource")
      .value(exampleResourceId)
      .operator("stringEquals")
      .build();

PolicyResource policyResources = new PolicyResource.Builder()
      .addAttributes(accountIdResourceAttribute)
      .addAttributes(serviceNameResourceAttribute)
      .build();

CreatePolicyOptions options = new CreatePolicyOptions.Builder()
      .type("authorization")
      .subjects(Arrays.asList(policySubjects))
      .roles(Arrays.asList(policyRoles))
      .resources(Arrays.asList(policyResources))
      .build();

Response<Policy> response = service.createPolicy(options).execute();
Policy policy = response.getResult();

System.out.println(policy);
```
{: java}
{: codeblock}

```javascript
const policySubjects = [
  {
    attributes: [
      {
        name: 'accountId',
        value: exampleAccounId,
      },
      {
        name: 'serviceName',
        value: "metrics-router",
      }
    ],
  },
];
const policyRoles = [
  {
    role_id: 'crn:v1:bluemix:public:sysdig-monitor::::serviceRole:Publisher',
  },
];
const accountIdResourceAttribute = {
  name: 'accountId',
  value: exampleAccountId,
  operator: 'stringEquals',
};
const serviceNameResourceAttribute = {
  name: 'serviceName',
  value: "sysdig-monitor"",
  operator: 'stringEquals'
};

const policyResources = [
  {
    attributes: [
      accountIdResourceAttribute,
      serviceNameResourceAttribute
    ],
  },
];
const params = {
  type: 'authorization',
  subjects: policySubjects,
  roles: policyRoles,
  resources: policyResources,
};

iamPolicyManagementService.createPolicy(params)
  .then(res => {
    examplePolicyId = res.result.id;
    console.log(JSON.stringify(res.result, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
policy_subjects = PolicySubject(
    attributes=[SubjectAttribute(name='accountId', value=example_account_id),
                SubjectAttribute(name='serviceName', value="metrics-router")
                ])
policy_roles = PolicyRole(
    role_id='crn:v1:bluemix:public:sysdig-monitor::::serviceRole:Publisher')
account_id_resource_attribute = ResourceAttribute(
    name='accountId', value=example_account_id)
service_name_resource_attribute = ResourceAttribute(
    name='serviceName', value="sysdig-monitor")
policy_resources = PolicyResource(
    attributes=[account_id_resource_attribute,
                service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
    type='authorization',
    subjects=[policy_subjects],
    roles=[policy_roles],
    resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
accountSubjectAttribute := &iampolicymanagementv1.SubjectAttribute{
    Name:  core.StringPtr("accountId"),
    Value: &exampleAccountID,
    Operator: core.StringPtr("stringEquals"),
}
serviceNameSubjectAttribute := &iampolicymanagementv1.SubjectAttribute{
    Name:  core.StringPtr("serviceName"),
    Value: "metrics-router",
    Operator: core.StringPtr("stringEquals"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
    Attributes: []iampolicymanagementv1.SubjectAttribute{*accountSubjectAttribute,
        *serviceNameSubjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
    RoleID: core.StringPtr("crn:v1:bluemix:public:sysdig-monitor::::serviceRole:Publisher"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("accountId"),
    Value:    core.StringPtr(exampleAccountID),
    Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
    Name:     core.StringPtr("serviceName"),
    Value:    core.StringPtr("sysdig-monitor"),
    Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
    Attributes: []iampolicymanagementv1.ResourceAttribute{
        *accountIDResourceAttribute, *serviceNameResourceAttribute},
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
    "authorization",
    []iampolicymanagementv1.PolicySubject{*policySubjects},
    []iampolicymanagementv1.PolicyRole{*policyRoles},
    []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
    panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}


## Removing an authorization in the console
{: #iam-service-auth-remove-auth-ui}
{: ui}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

1. In the {{site.data.keyword.cloud_notm}} console, click **Manage** &gt; **Access (IAM)**, and select **Authorizations**.
2. Identify the row for the authorization that you want to remove from the account.
3. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") > **Remove**.
4. Select **Remove**.

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using the CLI
{: #iam-service-auth-remove-auth-cli}
{: cli}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

The following sample deletes an authorization policy:
```sh
ibmcloud iam authorization-policy-delete 12345678-abcd-1a2b-a1b2-1234567890ab
```
{: codeblock}

For more information about all of the parameters that are available for this command, see [ibmcloud iam authorization-policy-delete](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_authorization_policy_delete).

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using the API
{: #iam-service-auth-remove-auth-api}
{: api}

You can remove any authorization between services in the account if you are assigned the `Administrator` role on the target service. If you remove any access policies created by the source service for its dependent services, the source service is unable to complete the workflow or access the target service.

To delete an authorization policy, use the [IAM Policy Management API](/apidocs/iam-policy-management#delete-policy) as in the following sample request:

```bash
curl -X DELETE 'https://iam.cloud.ibm.com/v1/policies/$POLICY_ID' \
-H 'Authorization: Bearer $TOKEN' \
-H 'Content-Type: application/json'
```
{: curl}
{: codeblock}

```java
DeletePolicyOptions options = new DeletePolicyOptions.Builder()
        .policyId(examplePolicyId)
        .build();

service.deletePolicy(options).execute();
```
{: java}
{: codeblock}

```javascript
const params = {
  policyId: examplePolicyId,
};

iamPolicyManagementService.deletePolicy(params)
  .then(res => {
    console.log(JSON.stringify(res, null, 2));
  })
  .catch(err => {
    console.warn(err)
  });
```
{: javascript}
{: codeblock}

```python
response = iam_policy_management_service.delete_policy(
  policy_id=example_policy_id
).get_result()

print(json.dumps(response, indent=2))
```
{: python}
{: codeblock}

```go
options := iamPolicyManagementService.NewDeletePolicyOptions(
  examplePolicyID,
)

response, err := iamPolicyManagementService.DeletePolicy(options)
if err != nil {
  panic(err)
}
```
{: go}
{: codeblock}

If the source service is removed from the account, any policies that are created by that service for its dependent services are deleted automatically. Similarly, if the dependent service is removed from the account, any access policies that are delegated to that service are also deleted.
{: note}

## Removing an authorization by using Terraform
{: #iam-service-auth-remove-auth-tf}
{: terraform}

If you want to remove an authorization by using Terraform, you need to delete the argument from the `main.tf` file. After you delete the argument, provision your file by using the following steps:

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}
