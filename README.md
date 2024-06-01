# Next.js Application Deployment on AWS ECS

This repository contains the configuration for deploying a Next.js application to AWS Elastic Container Service (ECS) using AWS Fargate. The deployment process is automated with GitHub Actions.

## Prerequisites

Before you start, make sure you have the following:

- An AWS account
- A GitHub repository with your Next.js application

## Setup

1. **Set up GitHub Secrets:**

   In your GitHub repository, navigate to `Settings > Secrets and variables > Actions` and add the following secrets:

   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_ACCOUNT_ID`

2. **Grab Subnet and Security Group IDs:**

   Ensure you have the subnet ID and security group ID where your ECS tasks will run. These will be used in the workflow.

## Workflow Details

The GitHub Actions workflow is triggered on `push` and `workflow_dispatch` events. It performs the following steps:

1. **AWS Authentication:** Authenticates with AWS using the provided credentials.
2. **Checkout Code:** Checks out the repository code.
3. **Setup Docker buildx:** Sets up Docker buildx, which is useful for caching image layers in the build step.
4. **Docker Login to AWS ECR:** Logs in to Amazon Elastic Container Registry (ECR).
5. **Create AWS ECR Repo:** Creates an ECR repository if it doesn't exist.
6. **Docker Build & Push:** Builds the Docker image and pushes it to the ECR repository. Configured to use layer caching if it exists.
7. **Create AWS ECS Cluster:** Creates an ECS cluster (continues on error if it already exists).
8. **Register Task Definition:** Registers the ECS task definition.
9. **Create/Update ECS Service:** Creates or updates the ECS service.
