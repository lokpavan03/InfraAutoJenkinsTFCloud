# Azure Infrastructure Automation with Jenkins and Terraform Cloud

<span style="color:black;">Contents</span>
- [Flow Diagram](#Flow-Diagram)
- [Jenkins setup from Docker](#Jenkins-setup-from-Docker)
- [Terraform Cloud setup](#Terraform-Cloud-setup)
- [Terraform Scripts](#Terraform-Scripts)
- [Jenkins Pipeline](#Jenkins-Pipeline)
- [Azure Resources Validation](#Azure-Resources-Validation)

## _**Flow Diagram**_
![Jenkins Docker](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/FlowChart.JPG?raw=true)

## _**Jenkins setup from Docker**_
1. Install the Docker Engine from the following URL **[DockerEngine](https://docs.docker.com/engine/install/)** as per the environment.
2. If you are windows user skip step 1 and install the Docker Desktop from the following URL **[DockerDesktop](https://docs.docker.com/docker-for-windows/install/)**
3. Login to the Docker Hub with credentials if you don't have account create a new one from the following URL **[DockerHUB](https://www.docker.com/)**
4. Open the command promt and login to the Docker Hub with the below command by using the credentials

            * docker login
            
5. Once login successfull, seach for the jenkins images by using the below command

            * docker search jenkins
            
6. From the list download the jenkins/jenkins image by using the below command

            * docker pull jenkins/jenkins
            
7. Run the Jenkins container by using the below command

            * docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins
            
   Note1: Here two port mappings happened one is 8080 and 50000 if the port is already used then choose the another port
   Note2: Copy the Jenkins Password from the command prompt to unlock the Jenkins
8. Once the container is up and running state. Open the browser and hit the below URL

             **http://localhost:8080**

![Jenkins Docker](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/docker.gif?raw=true)

9. Install the required plugins while setting up Jenkins and finish the basic setup.
10.Go to the Jenkins Dashboard -> Manage Jenkins -> Manage Plugins, under the Available plugins tab search for the "Blue Ocean" and "Active Choices" plugins and install it with out restart.

![Jenkins Plugins Installation](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/Plugins_Installation.gif?raw=true)

10.For test the Blue Ocean UI hit the below URL

             **http://localhost:8080/blue**

![Jenkins Blue](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/BlueOcean.gif?raw=true)

## _**Terraform Cloud setup**_
1. Create a Terraform Cloud account use the following URL **[TerraformCloud](https://www.terraform.io/cloud)** if account doesn't exists.
2. Once the Terraform Cloud account created login to the Terraform Cloud portal with Username and Password.
3. Create an organization if you are new to Terraform cloud or use the existing organization.
4. Create a workspace while creating it choose API_driven workflow environment type and provide the workspace name.

![Terraform_Cloud](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/TerraformWorkspace.gif?raw=true)

6. Setup API_TOKEN for GitHub to Terraform Cloud connection setup
7. Go to workspace -> User Settings -> Under the User options right top corner -> Tokens -> Create an API Token and name it -> Copy the Token.
8. Save the token as TF_API_TOKEN in GitHub Secrets and provide the secret under the terraform configuration provider in **main.tf** file.
9. Service Principal login needs the following variables and get the values from the Azure App

          * subscription_id
          * client_id
          * client_secret
          * tenant_id

![Terraform_Token](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/TerraformToken.gif?raw=true)

## _**Terraform Scripts**_
1. Create the Scripts as per the Azure resources requirement.
2. In Terraform **main.tf** is the main file it contains the Terraform Cloud Configuration block, Azure resource provider block and resoures block.
3. In Terraform **variables.tf** contains all the variable declaration information.

![Terraform_Scripts](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/TerraformScripts.gif?raw=true)

## _**Jenkins Pipeline**_
1. Create a New Item in the Jenkins dashboard and choose the pipeline job and provide name for it.

![Jenkins Pipeline](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/PipelineJob.gif?raw=true)

3. Generate the Jenkins pipeline script using syntax generator.
4. Once script is reade, save the file as Jenkinsfile and store it in GitHub repository.
5. Run the Jenkinsfile from the pipeline through SCM.

![Jenkinsfile](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/SCM_Jenkinsfile.gif?raw=true)

6. Run the Jenkins Pipeline Job with Build Parameters and provide the necessary inputs.

![JenkinsPipelineRun](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/JenkinsJobParams.gif?raw=true)

## _**Azure Resource Validation**_
1. Login to the Azure Portal **[AzurePortal](https://portal.azure.com)** with your credentials
2. Go to resouce group and check for created resources.
3. Validate whether the resources exists or not.

![Azure Resources Validation](https://github.com/lokpavan03/InfraAutoJenkinsTFCloud/blob/master/jpgs/Validation.gif?raw=true)
