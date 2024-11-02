# Notes

We cloned some code branch from: `gitops-aks-terraform-infra-repo` for using a terraform manifest that was already created to make resources with Azure.

This was cloned into `projects/section-4`.

In this repo we have a few files:

## Understanding Terraform Files and structure

Once we are familiar with the files and structure, we'll deploy the infrastructure.

There is a main.tf file, which is the main file for writing the terraform code. There is also a readme file with various commands to launch the infra.

Then there's a variable file to define the variables we'll use in the terraform files.

Then there's a vars directory, where we define all the variable values.

### In main.tf:

- first line is a comment; should be specific to understanding the terraform project structure overall; like `This file contains terraform code to create Azure Kubernetes Cluster`.
- Then there's a provider block which defines a plugin for the terraform code to interact with a specific cloud provider. There is a features block for azure, and this is a mandatory block for azure. There is official documentation to show which features should be used like api management, app configuration, application insights, cognitive account, etc. These are needed for our example, so we leave it blank. If we don't provide skip_provider_registration, we'd need to add in several other actions we don't need for the example.
- The next tag defines a resource group
- Then there's a kubernetes cluster defined, and its associated to the resource group
- Then there's a node pool, because we need a system and a user node for kubernetes. We define the number of system nodes.
- THere's also a system assigned identity to the cluster
- We are also usign a network plugin for azure.
- Then there's a cluster node pool defined for the user nodes.

So we defined:

- a resource group
- a kubernetes cluster in that resource group
- two types of nodes within the kubernetes cluster

### in Variables.tf:

there are variable names defined in this file, with descriptions and types provided. Its also helpful to give a comment to these variables.

YOu could provide a default value here also, but we do this separately.

Once you see the names, you can see where they are used in the main.tf file.

### Terraform.tfvars

Then you can look at this file to see where the default values are for the various variables.

This means we only need to update the names in a single place.

One note is we are using the Standard_D2_v2 instance type in Azure for the kubernetes nodes. This is a part of the free tier. Also the standard_D1_v2 is available on the free tier too.

Check out the instance sizes on the azure docs site.

Again, providing a meaningful comment can be helpful.

## Running the Terraform Code

We are going to run this to create the cluster.

Within the readme file, there are commands to run, but one of the pre-requisites is to authenticate using azure cloud from the cli, with the command `az login`.

NOTE: I actually had to use `az login --allow-no-subscriptions` because I don't have a subscription associated with my account.
