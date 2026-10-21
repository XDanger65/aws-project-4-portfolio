# AWS Serverless Portfolio Project

## Overview
A serverless application built using AWS SAM, AWS Lambda,
Amazon API Gateway, and AWS CloudFormation.

## Architecture
Client -> Amazon API Gateway -> AWS Lambda -> JSON response

## Technologies
- AWS Lambda
- Amazon API Gateway
- AWS SAM CLI
- AWS CloudFormation
- Python 3.13
- Git and GitHub

## Live API
https://plxuw3w49l.execute-api.us-east-1.amazonaws.com/Prod/hello/

## Test Result
HTTP GET request returns:

    {"message": "hello world"}

## Deployment
Build the application:

    sam build

Validate the template:

    sam validate

Deploy the application:

    sam deploy

## Cleanup
To remove the AWS resources when finished:

    sam delete --stack-name aws-project-4-portfolio --region us-east-1
