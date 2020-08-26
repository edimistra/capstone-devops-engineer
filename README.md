# Capstone Cloud Devops Engineer
Building a CI/CD Pipeline with Jenkins, Docker, Kubernetes on AWS: ECS, EKS

## Project Tasks:

* Use Jenkins
* Use the nginx hello app as a Docker Application - <https://github.com/nginxinc/NGINX-Demos/tree/master/nginx-hello>
* Applying the Blue/Green deployment
* Use ECS for uploading Docker image
* Used CloudFormation to create a Kubernetes cluster on EKS
* Configured the EC2 instance to run Jenkins and intalled EKS tools
* Set up all the steps that the pipeline will  include
* Added a Linting step
* Tested the pipeline

## Files Included

### Deployment folder
* ``` blue-controller.yaml ``` YAML file for the Blue deployment
* ``` green-controller.yaml ``` YAML file for the Green deployment

### Service folder
* ``` blue-service.yaml ``` YAML file for the Blue service corresponding to the Blue deployment
* ``` green-service.yaml ``` YAML file for the Green service corresponding to the Green deployment

### EKS folder
* ``` create-eks-cluster.yaml ``` CloudFormation file that creates the EKS Cluster, the cluster nodes, and the role associated to them
* ``` eks-cluster-parameters.json ``` CloudFormation flie with the parameters used in ``` create-eks-cluster.yaml ```

### nginx-hello folder
* Files related to the nginx-hello app - <https://github.com/nginxinc/NGINX-Demos/tree/master/nginx-hello>
* NGINX webserver that serves a simple page containing its hostname, IP address and port as wells as the request URI and the local time of the webserver.

### support_scripts folder
* ``` create.sh ``` and ``` update.sh ``` are used to create and update a CloudFormation stack. They are used in the command line to deploy the EKS Cluster

Usage:

``` ./create.sh eks-cluster ../EKS/create-eks-cluster.yaml ../EKS/eks-cluster-parameters.json ```

``` ./update.sh eks-cluster ../EKS/create-eks-cluster.yaml ../EKS/eks-cluster-parameters.json ```

### Dockerfile
* Dockerfile used to containerize the nginx-hello app

### Jenkinsfile
* Contains the stages and steps used by Jenkins to build the pipeline

### Screenshots
* aws-cloudformation-created-eks-cluster
* aws-ecs-docker-pushed-container
* aws-eks-cluster
* deployed_app_blue
* deployed-app-green
* jenkins-pipeline-all-steps-passed
* jenkins-pipeline-waiting-step-blue-green
* lint-step-failing

## Pipeline stages
* Lint HTML
* Docker Build
* Push Docker Image to AWS ECR
* Create the cluster configuration file
* Set current kubectl context
* Deploy Blue Container
* Deploy Green Container
* Create the service in the cluster, redirect to blue
* Wait for user approval
* Create the service in the cluster, redirect to green

## Important notes

* A custom AMI previously built with Jenkins already installed was used to expedite the delivery of this project. That custom AMI was created by myself during the Module 4
* Such image have been manually configured in order to fulfill the requirements of this project, such as setting at least 2 subnets in different AZs in order to create the EKS Cluster, installing kubectl, etc.
* In order to run this project you will need to provide your own EC2 instance with Jenkins and the tools needed to install EKS
