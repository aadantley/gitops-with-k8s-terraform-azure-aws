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
