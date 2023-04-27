# tf-devops-modules
Deploys an Ubuntu 22.04.2 LTS virtual machine to VMware from a template file prepared by packer, as well as modifiying it with customization and adding additional drives, mounting and formatting them, there are multiple variants to choose from in the modules folder, i.e. a plain ubuntu machine or a CS machine.

## Deploying a Virtual Machine using Terraform
This guide will walk you through the steps to deploy a Virtual Machine using Terraform via a GitHub runner. The runner is required to run Terraform in a GitHub Action.

## Prerequisites
Before proceeding, ensure that you have the following actions completed:
```code
- Clone this repository to your own company GitHub account and rename the repository to be something relevant to what you are deploying
- To clone the GitHub repository using the CLI use following command:
    $ git clone https://github.com/Joeharrison94/tf-vsphere-module.git
```
## Editing the main.tf.example file
Open the main.tf.example file located in the root directory of the repository and modify the values for the variables as per your requirements. These variables are used to configure the Virtual Machine that will be deployed. Once you have finalised your changes rename the file to main.tf and push your changes to your repo. this will trigger the GitHub action and build it.

## Values to modify
### Key / Value Table example for a deployment
### DO NOT CHANGE ANY VALUES NOT LISTED IN THE TABLE BELOW
| Variable | Description | Example |
|----------|-------------|-------------|
| `source` | The source to use from the modules folder | source = "./modules/vsphere-cs-terraform" |
| `vsphere_cluster` | The vSphere cluster to deploy the VM in | vsphere_cluster = "CLUSTER1" |
| `vsphere_datasource` | The vSphere datastore to deploy the VM on | vsphere_datasource = "DATASTORE1" |
| `vsphere_network` | The vSphere port group to connect the VM to | vsphere_network = "MANGEMENT" |
| `vsphere_template` | The name of the vSphere template to use for the VM | vsphere_template = "Ubnt-2204_02-2304210840" |
| `deployment_name` | The name to give the deployed VM in VMware and the hostname | "UBNT-SERVER-01" |
| `deployment_domain` | The LOCAL domain name to use for the VM, not a domain join | deployment_domain = "ubnt.local" | 
| `deployment_cpu` | The number of CPUs to allocate to the VM | deployment_cpu = "4" |
| `deployment_ram_mb` | The amount of RAM to allocate to the VM, in MB | deployment_ram_mb = "8192" |
| `deployment_additional_disks` | A list of additional disks to attach to the VM | This is an array, see example in file |
| `deployment_ip` | The IP address to assign to the VM | deployment_ip = "10.1.2.3" | 
| `deployment_subnet` | The subnet mask to use for the VM | deployment_subnet = "24" |
| `deployment_gateway` | The default gateway to use for the VM | deployment_gateway = "10.1.2.1" |
| `dns_server_list` | A list of DNS servers to use for the VM | dns_server_list = [ "1.1.1.1" ] |

## WARNING
Once you have modified the values in your main.tf file and pushed your changes to the remote repository on GitHub, the GitHub Action will be triggered and automatically deploy the VM using the new values. You can monitor the status of the deployment by checking the Actions tab on your GitHub repository. Once the deployment is complete, you should be able to access your new VM. Your default login credentials for the new machine are stored in Thycotic, ensure you login and change the password to something sufficient for production.
