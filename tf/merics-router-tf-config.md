---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-22"

keywords:

subcollection: metrics-router

---

{{site.data.keyword.attribute-definition-list}}



# Configuring {{site.data.keyword.at_short}} in the account by using Terraform
{: #metrics_router-tf-config}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments that follow Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.metrics_router_full_notm}} resources by using HashiCorp Configuration Language (HCL).
{: shortdesc}


Looking for a managed Terraform on {{site.data.keyword.cloud_notm}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't need to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud_notm}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can install from the {{site.data.keyword.cloud_notm}} catalog.
{: tip}

Before you begin, ensure that you have the [required access](/docs/metrics-router?topic=metrics-router-iam) to create and work with {{site.data.keyword.metrics_router_full_notm}} resources.

## Step 1. Install the Terraform CLI
{: #terraform-install-cli}

Complete the following steps to install the Terraform CLI:

1. Create a terraform folder on your local machine, and navigate to your terraform folder.

    ```sh
    mkdir terraform && cd terraform
    ```
    {: pre}

2. Download the Terraform version that you want. For example, you can download `terraform_0.15.5_darwin_amd64.zip` for a MacOS.

    The IBM Cloud Provider plug-in for Terraform currently supports Terraform version 0.12.x, 0.13.x, and 0.14.x only. Make sure to select a supported Terraform version.

3. Extract the Terraform zip file and copy the files to your terraform directory.

4. Set the environment PATH variable to your Terraform files.

    ```sh
    export PATH=$PATH:<terraform-directory>/terraform
    ```
    {: codeblock}

5. Verify that the installation is successful by using a terraform command.

    ```sh
    ./terraform
    ```
    {: pre}


## Step 2. Set up the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-setup-ibm-plugin}

After the Terraform CLI installation is complete, you must set up the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform so that you can start working with resources and services in IBM Cloud. For a list of supported versions, see the [{{site.data.keyword.cloud_notm}} Provider plug-in releases](https://github.com/IBM-Cloud/terraform-provider-ibm/releases){: external}.

The setup of the {{site.data.keyword.cloud_notm}} Provider plug-in varies depending on the Terraform CLI version that you want to use. To run your Terraform configuration files with Terraform version 0.13.x or higher, installation of the {{site.data.keyword.cloud_notm}} Provider plug-in for Terraform is not required. For more information, see [Terraform v0.13.x and higher](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#install-provider-v13).

For example, to run your Terraform configuration files with Terraform version 0.13.x or higher, complete the following steps:
1. Create a `versions.tf` file and specify the {{site.data.keyword.cloud_notm}} Provider plug-in version that you want to use with the `version` parameter.

    ```terraform
    terraform {
        required_providers {
            ibm = {
                source = "IBM-Cloud/ibm"
                version = "<provider version>"
                }
        }
    }
    ```
    {: codeblock}

    For example:

    ```terraform
    terraform {
        required_version = ">= 0.15"
        required_providers {
            ibm = {
                source = "ibm-cloud/ibm"
                version = "1.41.0"
            }
        }
    }
    ```
    {: codeblock}

2. Store the `versions.tf` file in your Git repository or the folder where Terraform is set up.


If you are using Terraform on {{site.data.keyword.cloud_notm}} modules, you must add a `versions.tf` file to all the module folders. You can refer the Terraform provider block from the [provider registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest){: external}. You can use the [IBM Cloud Observability - Terraform Module](https://registry.terraform.io/modules/terraform-ibm-modules/observability/ibm/latest){: external} module to configure an instance.
{: note}



## Step 3. Configure the {{site.data.keyword.cloud_notm}} Provider plug-in
{: #terraform-config-ibm-plugin}

After you complete the set up, you must [configure the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference).

Before you can start working with Terraform on {{site.data.keyword.cloud_notm}}, you must retrieve the credentials and parameters that are required for a Terraform resource or data source, and specify them in the `provider` configuration. This configuration is used by the {{site.data.keyword.cloud_notm}} Provider plug-in to authenticate with the {{site.data.keyword.cloud_notm}} platform and to view, create, update, or delete {{site.data.keyword.cloud_notm}} resources and services.

The following table lists input parameters that you can set in the `provider` block of your Terraform on {{site.data.keyword.cloud_notm}} configuration file:

|Input parameter | Required / optional  | Description           |
|----------------|----------------------|-----------------------|
|`ibmcloud_api_key`| Required | The {{site.data.keyword.cloud_notm}} API key to authenticate with the {{site.data.keyword.cloud_notm}} platform. For more information, about how to create an API key, see [Creating an API key](/docs/account?topic=account-userapikey#create_user_key). You can specify the API key in the `provider` block or retrieve the value from the `IC_API_KEY` or `IBMCLOUD_API_KEY` environment variables. If both environment variables are defined, `IC_API_KEY` takes precedence. |
|`ibmcloud_timeout`| Optional | The number of seconds that you want to wait until the {{site.data.keyword.cloud_notm}} API is considered unavailable. The default value is `60`. You can specify the timeout in the `provider` block or retrieve the value from the `IC_TIMEOUT` or `IBMCLOUD_TIMEOUT` environment variables. If both variables are specified, `IC_TIMEOUT` takes precedence. |
|`region`| Optional | The {{site.data.keyword.cloud_notm}} region where you want to create your resources. If this value is not specified, `us-south` is used by default. You can specify the region in the `provider` block or retrieve the value from the `IBMCLOUD_REGION` or `IC_REGION` environment variables. If both environment variables are specified, `IC_REGION` takes precedence. |
{: caption="Table 1. List of input parameters that you can set in the provider block of your Terraform" caption-side="top"}

For more information on how to use environment variables, see [Using environment variables](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#env-vars).

You can [add multiple provider configurations within the same Terraform on the {{site.data.keyword.cloud_notm}} configuration file](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-provider-reference#multiple-providers) to create your {{site.data.keyword.cloud_notm}} resources with different provider parameters. For example, you can multiple providers so that you can use different input parameters, such as different regions, zones, infrastructure generations, or accounts to create the {{site.data.keyword.cloud_notm}} resources in your Terraform on {{site.data.keyword.cloud_notm}} configuration file. For more information, see [Multiple Provider Instances](https://www.terraform.io/docs/language/providers/configuration.html){: external}.


### Option 1. Creating a static `provider.tf` file
{: #terraform-config-ibm-plugin-static}

You can declare the input parameters in the `provider` block directly.

Because the `provider` block includes sensitive information, do not commit this file into a public source repository. To add version control to your provider configuration, use a local [`terraform.tfvars` file](#tf-variables).
{: important}

Complete the following steps:

1. Create a `provider.tf` file and specify the input parameters that are required for your resource or data source.

    ```terraform
    provider "ibm" {
        ibmcloud_api_key = "<api_key>"
        region = "<region>"
    }
    ```
    {: codeblock}


### Option 2. Referencing credentials from a Terraform tfvars file
{: #terraform-config-ibm-plugin-tfvars}

You can store sensitive information, such as credentials, in a local `terraform.tfvars` file and reference these credentials in your `provider` block.

Do not commit the `terraform.tfvars` into a public source repository. This file is meant to be stored in your local machine only.
{: important}

1. Create a `terraform.tfvars` file on your local machine and add the input parameters that are required for your resource or data source.

    ```terraform
    ibmcloud_api_key = "<ibmcloud_api_key>"
    region = "region"
    ```
    {: codeblock}

2. Create a `provider.tf` file and use Terraform interpolation syntax to reference the variables from the `terraform.tfvars`.

    ```terraform
    variable "ibmcloud_api_key" {}
    variable "region" {}

    provider "ibm" {
        ibmcloud_api_key    = var.ibmcloud_api_key
        region = var.region
    }
    ```
    {: codeblock}


## Step 4. Initialize the Terraform CLI.
{: #terraform-init-tf-cli}

Next, initialize the Terraform CLI. Run the following command:

```sh
./terraform init
```
{: pre}

You should see the following message: `Terraform has been successfully initialized!`.


## Step 5. Create a variables file
{: #terraform-vars-tf}

Create a variables file that is named `variables.tf` to include hard-coded values.

The following sample lists variables that you define:

```terraform
variable "target_type" {
  description = "Type of resource that can be defined as a target. Valid values are: `sysdig-monitor`"
  type        = string
}

variable "cos_bucket_name" {
  description = "Name of the Monitoring instance"
  type        = string
}

variable "cos_target_crn" {
  description = "CRN of the Monitoring instance"
  type        = string
}

variable "cos_endpoint" {
  description = "Private endpoint of the Cloud Object Storage bucket"
  type        = string
}

variable "metrics_router_metadata_region_primary" {
  description = "Location where the metadata configuration is stored"
  type = string
  default = "us-south"
}
```
{: codeblock}


To see the list of valid regions, see [Locations](/docs/metrics-router?topic=metrics-router-regions#regions-metrics_router).


## Step 6. Create a Terraform configuration file
{: #terraform-main-tf}

Next, create a Terraform configuration file that is named `main.tf`. In this file, you configure {{site.data.keyword.metrics_router_full_notm}} by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

The following code shows a sample configuration file to define the account setting configuration:

```terraform
resource "ibm_metrics_router_settings" "metrics_router_settings" {
  metadata_region_primary = var.metrics_router_metadata_region_primary
  default_targets = ["comma-separated-list-of-target-ids"]
  permitted_target_regions  = ["comma-separated-list-of-locations"]
  private_api_endpoint_only = false

  # Optional but recommended lifecycle flag
  lifecycle {
    create_before_destroy = true
  }
}
```
{: codeblock}

The following code shows sample configurations to define a target:

```terraform
# Target type: cloud-object-storage
# Using service to service authorization
resource "ibm_metrics_router_target" "metrics_router_target" {
  cos_endpoint {
     endpoint = var.cos_endpoint
     target_crn = var.cos_target_crn
     bucket = var.cos_bucket_name
     service_to_service_enabled = true
  }
  name = "<Target-Name>"
  target_type = "cloud_object_storage"
  region = "us-south"
}

# Target type: cloud-object-storage
# Using a service ID Api key
resource "ibm_metrics_router_target" "metrics_router_target" {
  cos_endpoint {
     endpoint = var.cos_endpoint
     target_crn = var.cos_target_crn
     bucket = var.cos_bucket_name
     api_key = "api_key"
  }
  name = "<Target-Name>"
  target_type = "cloud_object_storage"
  region = "us-south"
}

# Target type: logdna
# Using an ingestion key
resource "ibm_metrics_router_target" "metrics_router_logdna_target" {
  logdna_endpoint {
    target_crn = "crn:v1:bluemix:public:logdna:us-south:a/11111111111111111111111111111111:22222222-2222-2222-2222-222222222222::"
    ingestion_key = "xxxxxxxxxxxxxx"
  }
  name = "<Target-Name>"
  target_type = "logdna"
  region = "us-south"
}
```
{: codeblock}

The following code shows sample configurations to define a route:

```terraform
## Create a route to route auditing events from Frankfurt

resource "ibm_metrics_router_route" "metrics_router_route_instance" {
  lifecycle {
    create_before_destroy = true
  }
  name = "<Route-Name>"
  rules {
    target_ids = [ibm_metrics_router_target.metrics_router_target.id]
    locations = ["eu-de"]
  }
}

## Create a route to route auditing events from 2 regions and also global events.

resource "ibm_metrics_router_route" "metrics_router_route_instance-global" {
  name = var.route_name-global

  rules {
    target_ids = [ibm_metrics_router_target.metrics_router_target-global.id]
    locations = ["global", "us-south", "eu-de"]
  }
}
```
{: codeblock}


## Step 7. Provision resources
{: #terraform-provision}

Complete the following steps:

1. Initialize the Terraform CLI.

    ```sh
    ./terraform init
    ```
    {: pre}

2. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.at_short}} instance, the resource Key, and IAM access policy in your account.

    ```sh
    ./terraform plan
    ```
    {: pre}

3. Create the resources.

    ```sh
    ./terraform apply
    ```
    {: pre}

    To delete resources, run `./terraform destroy`.
    {: tip}


## What's next?
{: #terraform_setup_next}


Verify that the resources are created.
