# Objective
Completely automated wireguard deployment on Azure

## Tasks
- [ ] Create VPS
- [ ] Create red hat virtual machine
- [ ] Apply wireguard ansible role
- [ ] Create one client configuration
- [ ] Create QR code for wireguard tunnel import 


## Software used
Terraform v1.0.10 on darwin_amd64  
azure-cli  
  "azure-cli": "2.30.0",  
  "azure-cli-core": "2.30.0",  
  "azure-cli-telemetry": "1.0.6",  
  "extensions": {}   
terraform resource provider: hashicorp/azurerm v2.86.0
Visual Studio Code   
Azure Extension  
Azure Terraform Extension  

---

### General Notes
How will we maintain our terraform state? Just use terraform cloud for now
Need to create a CLI only workspace, otherwise this will conflict with the github actions runner
Created TF_API_TOKEN from terraform cloud and added to terraformtest repo
Need to get auth credentials for the github actions runner to my azure subscription
az account list
copy the value for "id" 
az account subscription show --subscription-id "<id>"
az ad sp create-for-rbac --name "TF-ServicePrincipal" --role="Contributor" --scopes="/subscriptions/XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXX"
add the resulting secrets to either the terraform cloud variables or into the github repo as secrets
ARM_CLIENT_ID: ${{ secrets.az_client_id }}
ARM_CLIENT_SECRET: ${{ secrets.az_client_secret }}
ARM_SUBSCRIPTION_ID: ${{ secrets.az_subscription_id }}
ARM_TENANT_ID: ${{ secrets.az_tenant_id }}

Problem: myTFResourceGroup already exists from a previous tfstate, need to import and run terraform init before continuing with new tfstate
add resource to import.tf
az group show --name myTFResourceGroup --query id --output tsv 
terraform import azurerm_resource_group.myTFResourceGroup <output_from_previous_command>

Github actions workflow
On PR Run all the way through to terraform plan
On Merge run all the way through to terraform apply

Ran across a service principal permission issue, probably easier to delete previous resource group and start over


### Learning materials
https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-build?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-change?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-destroy?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-variables?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-outputs?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-remote?in=terraform/azure-get-started  
https://jloudon.com/cloud/Using-GitHub-Actions-and-Terraform-for-IaC-Automation/


#### Reference Links
https://docs.microsoft.com/en-us/cli/azure/  

https://www.terraform.io/docs/language/providers/requirements.html  
