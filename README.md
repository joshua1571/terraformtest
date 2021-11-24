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
Created TF_API_TOKEN from terraform cloud and added to terraformtest repo
Need to get auth credentials for the github actions runner to my azure subscription
Will need to create an azure service principal using the az command
az account show - to view the current subscription in use
az ad sp create-for-rbac --name terraformServicePrincipal --role Contributor
add the resulting tokens to repo secrets


### Learning materials
https://learn.hashicorp.com/tutorials/terraform/infrastructure-as-code?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-build?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-change?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-destroy?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-variables?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-outputs?in=terraform/azure-get-started  
https://learn.hashicorp.com/tutorials/terraform/azure-remote?in=terraform/azure-get-started  


#### Reference Links
https://docs.microsoft.com/en-us/cli/azure/  

https://www.terraform.io/docs/language/providers/requirements.html  
