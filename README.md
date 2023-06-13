# Portfolio Web App

This repository contains a simple HTML and CSS portfolio web app that has been Dockerized for easy deployment. Additionally, a Helm chart has been created to facilitate the deployment of the web app on a GKE cluster using Jenkins.

## Prerequisites

Before proceeding with the deployment, ensure that you have the following prerequisites set up:

- Docker installed on your local machine.
- Follow the steps to create a Google Kubernetes Engine (GKE) cluster using Terraform in my Infrastructure repository.
- Follow the steps to deploy Jenkins master and agent to interact with your GKE cluster in my Infrastructure repository.


## Configure Jenkins pipeline:

- Create a new Jenkins pipeline or modify an existing one to include the deployment steps for the portfolio web app.
- Choose Source Code Management to be GIT.
- Provide this repository URL https://github.com/Ahmadshata/App
- The Jenkinsfile provided in this repository includes the necessary steps to deploy the portfolio app Helm chart on your GKE cluster.

## Run the Jenkins pipeline:

Trigger the Jenkins pipeline to initiate the deployment process.
The pipeline will execute the necessary steps, including building the Docker image, pushing it to the container registry, and deploying the Helm chart on the GKE cluster.
Monitor the deployment:

Monitor the Jenkins pipeline console output to track the progress of the deployment.
Additionally, you can use the Kubernetes command-line tools or the GKE Console to verify the deployment status and check the running pods.

## Access the deployed web app:

Once the deployment is successful, you can access the portfolio web app by retrieving the external IP associated with the deployed service in the portfolio namespace.

```shell
kubectl get svc -n portfolio
```

