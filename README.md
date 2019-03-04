# Build Docker Enterprise 2.1 cluster on Azure using Terraform


## Overview

Files included in this repository will help you build a 5-node Docker Enterprise cluster
1. One Linux server that hosts both Docker UCP and DTR; also configured as the Swarm Manager / Kubernetes Master
2. Two Linux worker nodes in an availability set
3. Two Windows worker nodes in an availability set

## Pre-requisites to deploy this infrastructure

1. Azure subscription with access to create resources (free account will not work)
2. Docker Enterprise licence - you can get a free trial licence from [Docker Store](https://hub.docker.com/editions/enterprise/docker-ee-trial) which is valid for 30 days
3. Terraform v0.11, which you can download free from [HashiCorp site](https://www.terraform.io/downloads.html)

**The templates and scripts provided will perform a fully automated deployment of the Docker Enterprise cluster, hence in-depth knowledge of Terraform or scripting is not required to perform the steps**


## Get started

1. Clone the repository to your local system
2. Generate the SSH key pair files using `ssh-keygen -m PEM -f docker-key`
3. Copy the Docker licence key file in `lin-files` folder as `docker_subscription.lic`
4. Create Azure Service Principal to use with Terraform
   - az login
   - az account list (to see your subscriptions)
   - az account set -s "name of the subscription you want to use"
   - subscription_id="copy the id of the subscription you want to use"
   - az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}" 
    **Note the appID(CLIENT_ID), password(CLIENT_SECRET), tenant ID**
5. Update the variables in `terraform.tfvars` using the above information and as per your requirements

6. Run `terraform init` to initialise Terraform and download the required plugins
7. Run `terraform plan` to confirm there are no errors
8. Run `terraform apply` to build the infrastructure on Azure. It will take approximately 20 to 30 minutes to complete
9. Note the hostnames and IP addresses shared at the end of execution as you will need this to access the environment



