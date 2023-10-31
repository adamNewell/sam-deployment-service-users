# Functional/Architectural Requirements

Deliver four backend endpoints (no front end, no HTML) that will be the start of user management for a new application.
The endpoints shall create, read, update, and delete new users. The properties of a user object are left up to you.
x Enable appropriate authentication and validation on these endpoints.
The user’s data shall be stored in DynamoDB with primary and sort keys named ‘_pk0’ and ’_sk0’ respectively.
Deployment of these APIs can be provided through your preferred Infrastructure-As-Code framework.

## Required AWS services

* API Gateway
* DynamoDB

## Prohibited AWS services

* Lambda

    \**All other AWS services optional per your design*\*

## Deliverables

* IAC code to deploy.
* Deploy and test instructions
* Postman file we can use to exercise the deployed endpoints

## Solution

### Requirements

* AWS CLI
* AWS SAM CLI

### Deploy

* Ensure that you have a default AWS profile configured in your `~/.aws/credentials` file
* run `sam deploy`

### Postman Setup

* Import the postman collection `postman_collection.json`
* Set the environment variable `baseUrl` to the API Gateway URL output from the deploy step
* The CloudFormation output specifies a terminal command to run to get the api key to use as the `x-api-key` header value
    * It will look something like this: `aws apigateway get-api-key --api-key <api-key> --include-value --query "value"`
    * It may require you to run `aws configure` to set your default AWS profile

### Tear Down

* run `aws cloudformation delete-stack --stack-name <stack-name>`
* run `aws cloudformation list-stacks --query "StackSummaries[?contains(StackName,'STACK_NAME')].StackStatus"` to verify stack deletion
