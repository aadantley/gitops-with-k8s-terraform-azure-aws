# Notes

GitOps with Kubernetes and Terraform on Azure and AWS.

This will learn to create a GitOps pipeline for a mario game. We will implement this to be able to play it in the browser and deploy it with Azure Kubernetes services.

You can actually play this game through the browser.

We will use Kubernetes, Terraform, Azure cloud. The GitOps pipeline will be done in Yaml with Github actions.

We'll also use ArgoCD to make deployments on Kubernetes, where an actual pipeline will be made for this Mario project.

## Agenda

- bascis of GitOps DevOps, and DevSecOps
  - understanding the difference between the terms as they are common in enterprise environments
- Understanding the parts of the GitOps Case Study and prerequisites with Terraform Azure and AWS
  - We will create the infrastructure and create accounts in both Azure and AWS
- Clone the repo on the local system, then us GitOps pipeline with SonarQube to perform Static Code Analysis on the code.
  - Sonarqube is used to identify code quality issues in the source code on EC2
- Then we'll dockerize the game and build and push this image with a static tag to the container registry
  - we'll enhance to dynamic tags later
- Then we'll use aqua trivy to run container scans in the GitOps pipeline
  - Will be interesting to identify vulnerabilities here
- Then we'll use ArgoCD to deploy kubernetes clusters on Azure / AWS. This cluster will be created using terraform.
- Then we'll implement an end to end gitOps pipeline to tes the Continuous integration, continuous security, and continous deployment.
  - we'll make some changes to the mario project code to see how this pipeline updates the code.
- We'll execute the E2E pipeline to make sure the updates we did are seen in the deployment.

This will essentially recreate an enterprise pipeline for deployment.

## What Is GitOps

GitOps: a set of practices to leverage Git as a single source of truth for continuous delivery, which includes continuous integration, continous deployment, and continuous security. The core idea is to manage the deploymenet and operation of infrastructure and applications through version-controlled declarative configurations.

Principles:

- version control is the source of truth; all configuration, scripts, or policies must be tracked in Git.
- continuous delivery: promoting automaed continuous integration, deployment and security. This includes creating docker images automatically and deploying those images to k8s automatically. All of which is stored in the Git repo
- pull based deployment: the deployment changes are trigged by changes in the Git repository. Argo calls Git after every 3 minutes to check for changes.
- monitoring and observability: argo will detect any changes between the current state the state of the git repo.
- collaboration: facilitating collaboration through pull requests, allowing for code reviews, discussions, and approvals before these changes are added to the system.

## gitOps, DevOps, DevSecOps

Focus:

- gitOps focuses on operatiosn and deployments
- DevOps focuses on improving connections between Dev team and Operations team
- DevSecOps focuses on securing the application trhough the SDLC

Principles:

- gitOps: declarative configuration, version control as a source of truth, continuous delivery
- DevOps: collaboration, automation, CI/CD, IaC
- DevSecOps: integration of security practices, automation, collaboration, continuous security

All 3 use Git as the version control system

Key benefits:

- gitops: enhanced reliability, observability, and easy rollbacks
- DevOps: faster and more reliable software delivery
- DevSecOps: improved security posutre, early detection of vulnerabilities

Tooling:

- gitOps: flux, ArgoCD
- DevOps: jenkins, travis, Ci, Docker, etc.
- DevSecOps: OWASP ZAP, SonarQube, Trivy, Veracode, Microfocuse and others

Deployment model:

- pull-based deployment
- push-based deployment
- push-based deployment with security checks

Examples:

- managing K8s with ArgoCD
- using Jenkins for CICD pipelines
- integrating security scans into CICD pipelins with OWASP ZAP and SonarQube

## What is Terraform?

Terraform is a tool for building changing and versioning infrastructure safely and efficiently, with Terraform code. and This creates a blueprint for constructing and managing your entire application's servers, databases, and other tech resources, all of which live in the cloud.

Terraform structure is like blueprints for building digital resources, all of which are in the cloud, as terrraform is compatible with many different cloud providers.

Terraform configuration files: this is the file we write in hashicorp configuration language to build the environment / digital assets.

The files give a blueprint, then we use the command `terraform plan` to review the blueprint to understand what we have designed and to ensure there are no surprises. It will help you understand all of the parts of the house you'd want to build, and will also identify what resources will be created, without actually creating the resources.

`terraform apply` is the command to start building the infrastructure in the cloud. This will use the configuration files to create the servers databases and components.

Terraform then maintains a state file which is a detailed record of how the infrastructure looks at any point of time. This record is known as the terraform state.

Terraform destroy is a command to allow you to destroy all resources created.

## Case Study in Parts

Steps:

- use terraform to create infra in Azure and AWS.
  - we'll set up k8s in Azure, and an EC2 with SonarQube in AWS.
  - we'll go through the accounts and API token process too.
- We'll enable github actions for the repo and then clone the github repo to our system.
- Then we'll write a gitHub action file to run the SonarQube scane on the source code for SAST where SOnarQube is run on the EC2 instance in AWS.
- Then we'll dockerize the mario game, and push it to dockerhub with a static tag.
- We'll verify in docker hub the image has been pushed.
- Then we'll update the YAML file to generate dynamic tags
- then we'll create an application in ArgoCD and connect this to the gitHub repo, and also write a deployment yaml file.
- Then we'll deploy to Azure K8s service with ArgoCD.

Once we do each step, we'll implement the pipeline.

There are differences between GitOps and DevSecOps; so we can use the words above when they apply to this pipeline, as it is an integration of all 3 concepts.

## Creating an Azure account

creating an account with my aadantley@gmail.com account.
