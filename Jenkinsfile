pipeline {
    agent any
    parameters {
        string defaultValue: 'VM001-Jenkins', description: 'Please provide the VM Name', name: 'VirtualMachineName'
        string defaultValue: 'West Europe', description: 'Please Provide the Resource group location if you want to change', name: 'ResourceGroupLoaction'
        string defaultValue: 'TFCloudRG001', description: 'Please Provide the Resource group name if you want to change', name: 'RescourceGroupName'
        string defaultValue: 'subnet01', description: 'Please provide the Subnet Name if need change', name: 'SubNetName'
        string defaultValue: 'adminuser', description: 'Please provide the VM User Name', name: 'VMUserName'
        password defaultValue: 'Admin123', description: 'Please provide the password if you want change default', name: 'VMPassword'
    }
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitCreds', url: 'https://github.com/lokpavan03/jenkinstf.git']]])
            }
        }
        stage('TFvarsFile') {
            steps {
                    writeFile file: 'terraform.tfvars', text:  """resource_group_name = "${params.RescourceGroupName}"\n
                    resource_group_location = "${params.ResourceGroupLoaction}"\n
                    vnet_name = "${params.VirtualNetworkName}"\n
                    subnet_name = "${params.SubNetName}"\n
                    azure_virtual_machine_name = "${params.VirtualMachineName}"\n
                    admin_vm_username = "${params.VMUserName}"\n
                    admin_vm_password = "${params.VMPassword}"\n"""
            }
        }        
        stage('Terraform init') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Terraform plan') {
            steps {
                sh 'terraform plan'
            }
        }
        stage('Terraform Apply') {
            steps {
                sh 'terraform apply'
            }
        }                    
                    
    }
}

