Create a Serverless API
Project Overview
Built a serverless HTTP API on Amazon Web Services (AWS) using AWS Lambda and Amazon API Gateway. The API returns a plain-text Hello Serverless World! response and requires an API key for requests to the deployed endpoint.
- Cloud provider: Amazon Web Services (AWS)
- Region used: Asia Pacific (Hyderabad) — ap-south-2
- API type: API Gateway REST API
- Method: GET
- Stage: dev
- Lambda runtime: Node.js
- Status: Implemented and tested; project resources were subsequently deleted after evidence was captured.
Objectives
- Create and test an AWS Lambda function.
- Expose the function through an API Gateway REST API.
- Deploy the API to a named stage.
- Require an API key for requests.
- Verify the successful response using Postman.
Architecture
Client (Postman)
      |
      | GET /dev
      | x-api-key: <API_KEY>
      v
Amazon API Gateway REST API
      |
      | GET method (API key required)
      v
AWS Lambda: hello-serverless-world
      |
      v
HTTP 200 response
"Hello Serverless World!"


AWS Resources
Resource	Name / Configuration	Purpose
AWS Lambda function	hello-serverless-world	Returns the Hello World response
API Gateway REST API	hello-serverless-api	Provides the HTTP endpoint
Deployment stage	dev	Makes the API deployment callable
API key	hello-serverless-client-key	Identifies clients using the API
Usage plan	hello-serverless-usage-plan	Associates the API key with the deployed stage and defines throttling

Lambda Implementation
The Lambda handler returns HTTP-style response data for API Gateway.
export const handler = async (event) => {
    return {
        statusCode: 200,
        headers: {
            "Content-Type": "text/plain"
        },
        body: "Hello Serverless World!"
    };
};


Expected Lambda test result
The Lambda test completed successfully and returned:
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "text/plain"
  },
  "body": "Hello Serverless World!"
}


API Gateway Configuration
1. Created a Regional REST API named hello-serverless-api.
2. Created a GET method on the root resource (/).
3. Integrated the method with the hello-serverless-world Lambda function.
4. Deployed the API to the dev stage.
5. Enabled API Key Required for the GET method.
6. Redeployed the API after changing the method request setting.
API Key and Usage Plan
Created an API key named hello-serverless-client-key and a usage plan named hello-serverless-usage-plan.
- Associated the usage plan with hello-serverless-api at stage dev.
- Associated the API key with the usage plan.
- Configured a practice throttle of 5 requests per second and a burst limit of 10.
- Left the optional quota disabled.
Security note: API Gateway API keys and usage plans are intended for usage identification and throttling, not as a complete authentication or authorization solution. Production APIs should use an appropriate authorization mechanism where required. Never commit a real API key to a public repository.
Testing and Results
Lambda test
- Result: Succeeded
- Response body: Hello Serverless World!
Postman API test
- Method: GET
- Request: Deployed API invoke URL for stage dev
- Header: x-api-key: <API_KEY> (secret value omitted)
- Result: 200 OK
- Response body: Hello Serverless World!
The endpoint initially returned 403 Forbidden when called from a browser after API-key enforcement was enabled. This was expected because a normal browser navigation did not include the required x-api-key header. After checking the key and usage-plan associations, the request succeeded in Postman.
Key Concepts Learned
- Function as a Service (FaaS): Run code in response to events without managing the underlying servers.
- AWS Lambda: Executes the handler and returns the response.
- Amazon API Gateway: Exposes an API endpoint and routes requests to Lambda.
- Deployment stages: A deployed API must be associated with a stage such as dev to be invoked through its stage URL.
- API keys and usage plans: Help identify API consumers and apply request throttling and optional quotas.
- Postman: Sends requests with custom headers and verifies HTTP status codes and response bodies.
Answers to Project Questions
1. What is Function as a Service (FaaS)?
FaaS is a cloud computing model in which developers deploy individual functions that execute in response to events without provisioning or managing servers. AWS Lambda is an example.
2. How many languages are supported by AWS Lambda?
Lambda supports multiple managed runtimes, including Node.js, Python, Java, .NET, Go, and Ruby, as well as custom runtimes. Availability and supported versions can change, so check the current AWS Lambda runtime documentation for the exact list.
3. What is the maximum memory allocated to an AWS Lambda function?
AWS Lambda supports memory configuration up to 10,240 MB (10 GB). Confirm current limits in AWS documentation if using this answer for an assessment.
4. How many ways are there to deploy a Lambda function?
Common deployment approaches include the AWS Management Console, AWS CLI, AWS SDKs, AWS SAM, CloudFormation, Terraform, and CI/CD pipelines. These are deployment approaches rather than a fixed official count.
5. Name some Lambda triggers other than API Gateway.
Examples include Amazon S3 events, Amazon SQS, Amazon SNS, Amazon DynamoDB Streams, Amazon EventBridge, Amazon Kinesis, and other AWS service events.
6. How do you assign a role to Lambda?
Create or select an IAM execution role with only the permissions the function needs, then assign it under the function's configuration permissions. The basic execution policy typically allows writing logs to CloudWatch Logs.
7. How can an API Gateway endpoint be secured?
Options include IAM authorization, Amazon Cognito or another supported authorizer, Lambda authorizers, and API keys with usage plans. API keys alone should not be treated as strong authentication.
8. How do you add API Gateway as a Lambda trigger?
Create an API Gateway API and method, configure its integration to invoke the Lambda function, grant the required invocation permission, and deploy the API to a stage.
Cleanup and Cost Notes
After capturing the portfolio evidence, the API Gateway REST API, usage plan, API key, and Lambda function were deleted. The AWS Billing page showed an estimated total of USD $0.00 for October 2026 at the time it was checked; this was a pending estimate and could change as billing data updated.

Always check the AWS Billing console and other services for remaining resources. Deleting this project's resources does not remove unrelated resources from the AWS account.
Possible Improvements
- Rebuild the API using AWS SAM or Terraform to demonstrate Infrastructure as Code.
- Add structured logging and error handling.
- Add an appropriate authorizer for stronger authentication if required.
- Configure CloudWatch alarms and request monitoring.
- Add automated tests and a CI/CD deployment pipeline.
References
- AWS Lambda — Getting Started
- Amazon API Gateway — Getting Started
- Tutorial: Build a Lambda function with API Gateway
- Control access to API Gateway APIs
- AWS Lambda runtimes
