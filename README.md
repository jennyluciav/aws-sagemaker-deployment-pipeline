# Aws SageMaker Deployment Pipeline

## Introduction

This is a sample solution to build a deployment pipeline for Amazon SageMaker. This example could be useful for any organization looking to operationalize machine learning with native AWS development tools such as AWS CodePipeline, AWS CodeBuild and AWS CodeDeploy.

This solution provides a *Blue/Green*, also known as an *Canary deployment*, by creating an AWS Lambda API that calls into an Amazon SageMaker Endpoint for real-time inference.

##  Architecture

In the following diagram, you can view the continuous delivery stages of AWS CodePipeline.

1. Build Artifacts: Runs an AWS CodeBuild job to create AWS CloudFormation templates.
2. Train: Trains an Amazon SageMaker pipeline and Baseline Processing Job
3. Deploy Dev: Deploys a development Amazon SageMaker Endpoint
4. Deploy Prod: Deploys an Amazon API Gateway endpoint, and AWS Lambda function in front of Amazon SageMaker Endpoints using AWS CodeDeploy for blue/green deployment and rollback.

![code-pipeline](docs/code-pipeline.png)

###  Components Details

  - [**AWS CodePipeline**](https://aws.amazon.com/codepipeline/) – CodePipeline has various stages defined in CloudFormation, which step through which actions must be taken in which order to go from source code to creation of the production endpoint.
  - [**AWS CodeBuild**](https://aws.amazon.com/codebuild/) – This solution uses AWS CodeBuild to build the source code from GitHub.
  - [**Amazon S3**](https://aws.amazon.com/s3/) – Artifacts created throughout the pipeline as well as the data for the model is stored in an Simple Storage Service (S3) Bucket.
  - [**AWS CloudFormation**](https://aws.amazon.com/cloudformation/) – This solution uses the AWS CloudFormation Template language, in either YAML or JSON, to create each resource including a custom resource.
  - [**AWS Step Functions**](https://aws.amazon.com/step-functions/) – This solutions creates AWS StepFunctions to orchestrate Amazon SageMaker training and processing jobs.
  - [**Amazon SageMaker**](https://aws.amazon.com/sagemaker/) – This solution uses Amazon SageMaker to train and deploy the machine learning model.
  - [**AWS CodeDeploy**](https://aws.amazon.com/codedeploy/) – This solution uses AWS CodeDeploy to automate shifting traffic between two AWS Lambda functions.
  - [**Amazon API Gateway**](https://aws.amazon.com/api-gateway/) – This solutions creates an HTTPS REST API endpoint for AWS Lambda functions that invoke deployed Amazon SageMaker Endpoint.

