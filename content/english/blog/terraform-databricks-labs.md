---
title: "Terraform Databricks Labs"
date: 2021-08-14T00:00:00+01:00
description : "Terraform Databricks Labs"
type: blog
image: images/portfolio/terraform-databricks-labs/terraform-adb-labs-featured.png
author: Falek Miah
tags: ["Terraform", "Databricks", "Azure"]
draft: false
---

In late 2020, Databricks introduced [Databricks Labs](https://databricks.com/learn/labs) a collection of [Terraform Providers](https://registry.terraform.io/providers/databrickslabs/databricks/latest/docs) that gives you the ability to deploy nearly all Databricks resources onto Azure and Amazon Web Services (AWS) cloud platforms.  

Meaning you can deploy Databricks workspace, clusters, secrets, libraries, notebooks and automated jobs (and many more) at the time of provisioning the infrastructure, making it easy to manage and configure Databricks.  

This post will focus on Azure cloud platform but the concept is similar for AWS.  

## Assumption

I’m going to make the following assumptions: 

- You have basic understanding of Terraform components like Input Variable (.tf), Variable Definitions (.tfvars), Output files and Backend-Config. 
- You have basic understanding of Databricks components, like Workspace, Clusters, Token, Scopes.  

Let’s get started.  

## Create Terraform `Main.tf` file

You need to create a terraform `main.tf` file, then we can start adding content to it.  

First add the providers, both `azurerm` and `databrickslabs` is needed as required_providers.  

```terraform

  terraform {
    required_providers {
      azurerm = {
        source = "hashicorp/azurerm"
        version = "~>2.31.1"
      }
      databricks = {
        source  = "databrickslabs/databricks"
        version = "0.3.2"
      }
    }
  }

```

Then configure each provider, the `databricks` provider requires 'databricks_workspace.id' to be defined.  

```terraform

  provider "azurerm" {
      features {}
  }

  provider "databricks" {
    azure_workspace_resource_id = azurerm_databricks_workspace.databricks_workspace.id
  }

```

Next, you need to add the resource group.  We will use variables that are defined in the variable definitions (.tfvars) file.  

```terraform

  resource "azurerm_resource_group" "rg" {
    name     = var.resource_group_name
    location = var.azure_region
  }

```

Now you can start adding Databricks resources, firstly let's add Databricks workspace.  

```terraform

  resource "azurerm_databricks_workspace" "databricks_workspace" {
    name                        = var.databricks_name
    resource_group_name         = var.resource_group_name
    managed_resource_group_name = var.databricks_managed_resource_group_name
    location                    = var.azure_region
    sku                         = var.databricks_sku_name
  }

```

Now add Databricks secret scope to the workspace and generate a personal access token (pat) for 1 hour then store as a secret in the scope.  

```terraform

  resource "databricks_secret_scope" "secret_scope" {
    name = var.secret_scope_name
    initial_manage_principal = "users"
  }

  resource "databricks_token" "pat" {
    comment          = "Created from ${abspath(path.module)}"
    lifetime_seconds = 3600
  }

  resource "databricks_secret" "token" {
    string_value = databricks_token.pat.token_value
    scope        = databricks_secret_scope.secret_scope.name
    key          = var.databricks_token_name
  }

```

Next add a Databricks cluster and configure the libraries to include some packages.  

```terraform

  resource "databricks_cluster" "databricks_cluster_01" {
    cluster_name            = var.cluster_name
    spark_version           = var.spark_version
    node_type_id            = var.node_type_id
    autotermination_minutes = var.autotermination_minutes
    autoscale {
      min_workers = var.min_workers
      max_workers = var.max_workers
    }
    # Create Libraries
    library {
      pypi {
          package = "pyodbc"
          }
    }
    library {
      maven {
        coordinates = "com.microsoft.azure:spark-mssql-connector_2.12_3.0:1.0.0-alpha"
      }
    }
    custom_tags = {
      Department = "Data Engineering"
    }
  }

```

You can load notebooks directly to workspace when using Terraform, so let’s create and load a simple notebook using `content_base64` and `language` attributes.  The path is location of where the notebook will be stored, this is defined in the variable definitions (.tfvars) file.  

```terraform

  resource "databricks_notebook" "notebook" {
    content_base64 = base64encode("print('Welcome to Databricks-Labs notebook')")
    path      = var.notebook_path
    language  = "PYTHON"
  }

```

Finally, you need to define the backend configuration for where the Terraform state file will be stored.  This is optional if you are doing it locally for testing purposes.  

```terraform

  terraform {
      backend "azurerm" {
          key = "terraform.tfstate"
      }
  }
  data "terraform_remote_state" "platform" {
      backend = "azurerm"
      config = {
          key                  = var.platform_state_key_name
          container_name       = var.platform_state_container_name
          storage_account_name = var.platform_state_storage_account_name
          resource_group_name  = var.platform_state_resource_group_name
      }
  }

```

## Other Terraform files

You will need to create the `variables.tf` and `output.tf` (optional) files. I will not specify how to create these files but they will be available on **[GitHub](https://github.com/FalekMiah01/Infrastructure-IaC/tree/main/tf-databricks-labs)**.

## Create Terraform Variable Definitions (.tfvars) file

You need to create a `terraform-dblabs.tfvars` file, then we can start adding content to it.  The variable definitions (.tfvars) file will contain the values for the variables you defined in `main.tf` file.  

First add the backend configuration values for the Terraform state file storage and Azure resource.  

```terraform

  ## Terraform State
  platform_state_key_name             = "<Enter your state_file_name>"
  platform_state_container_name       = "<Enter your state_container_name>"
  platform_state_storage_account_name = "<Enter your state_storage_account_name>"
  platform_state_resource_group_name  = "<Enter your state_resource_group_name>"

  ## Azure Resource
  tenant_id           = "<Enter your tenant_id>"
  subscription_id     = "<Enter your subscription_id>"
  azure_short_region  = "uks"
  azure_region        = "UK South"
  resource_group_name = "rg-databrickslabs"

```

Then add the variable values for the Databricks content.  

```terraform

  databricks_name                        = "dbrickslabs-ws"
  databricks_managed_resource_group_name = "rg-databrickslabs-mrg"
  databricks_sku_name                    = "standard"
  secret_scope_name                      = "databrickslabs-scope"
  databricks_token_name                  = "databrickslabs-token"

  cluster_name                            = "databrickslabs-cluster"
  spark_version                           = "7.3.x-scala2.12"
  node_type_id                            = "Standard_DS3_v2"

  autotermination_minutes                 = "20"
  min_workers                             = "1"
  max_workers                             = "4"

  notebook_path                           = "/Shared/Demo/example_notebook"

```

# Execute Terraform Project

Now that the resources and Terraform files have been defined you can deploy the resources. 

### Login to Azure

Login into Azure using the Azure CLI and set the subscription of where you are deploying.  

```powershell

  az login
  az account set --subscription = '<enter_your_subscription_Id>'

```

### Terraform Init

Initialize the project using `Terraform Init` command which will downloads all of the required components for Azure and Databricks.

```powershell

  terraform init -backend-config="<backend-config>"
  terraform validate

```

### Terraform Plan

Now, execute the `Terraform Plan` command to see what will be created.

```powershell

  terraform plan -var-file="./terraform-dblabs.tfvars"

  Output:
  Plan: 7 to add, 0 to change, 0 to destroy.

```

### Terraform Apply

The plan shows there will be seven resources created, which is correct. So let's execute it using the `Terraform Apply` command, you may be prompted to confirm the action if so then enter `yes`.

```powershell

  terraform apply -var-file="./terraform-dblabs.tfvars"

  Output:
  Apply complete! Resources: 7 added, 0 changed, 0 destroyed.
  
```

# Review the Azure Databricks Resource 

Lets see the result of the Terraform execution.  

**Azure Resource**

{{<img src="/images/portfolio/terraform-databricks-labs/adb-labs-azure-resource.png" alt="adb-labs-azure-resource" width="700" align="center">}} <br><br>

 **Cluster and Libraries**

{{<img src="/images/portfolio/terraform-databricks-labs/adb-labs-cluster-libraries.png" alt="adb-labs-cluster-libraries" width="700" align="center">}} <br><br>

 **Personal Access Token for 1 hour**

{{<img src="/images/portfolio/terraform-databricks-labs/adb-labs-pat.png" alt="adb-labs-pat" width="700" align="center">}} <br><br>

**Sample Notebook**

{{<img src="/images/portfolio/terraform-databricks-labs/adb-labs-notebook.png" alt="adb-labs-notebook" width="700" align="center">}} <br><br>

# Summary

This post is intended to give you a flavour of what Databricks Labs provider can do in Terraform. 

We defined and deployed Azure resources and several Databricks components using Terraform.  Prior to Terraform Databricks Labs provider we would have had to create these Databricks components using a mix of ARM templates, JSON files and the Terraform Azure providers or just manually in Databricks.  

The Databricks Labs provider has reduce this approach and made it easier to read, manage and maintain by giving us the ability to provisioning these when the infrastructure is set up.  

Thanks for reading, I hope you found this post useful and helpful. 

All code files can be found on **[GitHub](https://github.com/FalekMiah01/Infrastructure-IaC/tree/main/tf-databricks-labs)**.  
