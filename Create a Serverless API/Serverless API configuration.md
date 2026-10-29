Create a Serverless API
AWS project | Serverless computing | Lambda + API Gateway

Built and tested a serverless HTTP API that returns Hello Serverless World!. The endpoint was protected with an API key and verified using Postman. The AWS project resources were deleted after testing and portfolio evidence was captured.

1. Project Overview
Detail	Configuration
Cloud provider	Amazon Web Services (AWS)
Region	Asia Pacific (Hyderabad), ap-south-2
API type	Amazon API Gateway REST API
HTTP method	GET
Deployment stage	dev
Lambda runtime	Node.js
Final test result	200 OK — Hello Serverless World!


2. Objectives
- Create and test an AWS Lambda function.
- Expose the function through an API Gateway REST API.
- Deploy the API to a stage.
- Require an API key for requests.
- Verify the endpoint using Postman.
3. Architecture
Postman client
    |
    | GET /dev
    | x-api-key: <API_KEY>
    v
Amazon API Gateway REST API
    |
    | GET method — API key required
    v
AWS Lambda: hello-serverless-world
    |
    v
HTTP 200 OK
Hello Serverless World!
AWS resources
Resource	Name	Purpose
AWS Lambda function	hello-serverless-world	Returns the response message
API Gateway REST API	hello-serverless-api	Exposes the HTTP endpoint
Deployment stage	dev	Makes the deployed API callable
API key	hello-serverless-client-key	Identifies the API consumer
Usage plan	hello-serverless-usage-plan	Associates the key with the stage and configures throttling


4. Lambda Implementation
The Lambda handler returns a successful response with a plain-text body.
export const handler = async (event) => {
    return {
        statusCode: 200,
        headers: {
            "Content-Type": "text/plain"
        },
        body: "Hello Serverless World!"
    };
};
Lambda test result
The Lambda test completed successfully (Succeeded) and returned:
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "text/plain"
  },
  "body": "Hello Serverless World!"
}
5. API Gateway Configuration
1. Created a Regional REST API named hello-serverless-api.
2. Created a GET method on the root resource (/).
3. Integrated the method with the hello-serverless-world Lambda function.
4. Deployed the API to the dev stage.
5. Set API Key Required to true for the GET method.
6. Redeployed the API so the security setting applied to the live stage.
6. API Key and Usage Plan
Created the API key hello-serverless-client-key and the usage plan hello-serverless-usage-plan.
Setting	Value
Associated API stage	hello-serverless-api → dev
Throttle rate	5 requests per second
Burst limit	10 requests
Quota	Disabled


The API key was associated with the usage plan, and the usage plan was associated with the deployed API stage.
Security note: API Gateway API keys and usage plans support consumer identification and throttling; they are not a complete authentication or authorization mechanism. For production APIs, use an appropriate authorizer when needed. Never publish an actual API key.

7. Testing and Results
Lambda test
Check	Result
Execution	Succeeded
Response body	Hello Serverless World!


Postman API test
Check	Result
Method	GET
Endpoint	API Gateway invoke URL for stage dev
Header	x-api-key: <API_KEY>
HTTP status	200 OK
Response body	Hello Serverless World!


After API-key enforcement was enabled, opening the endpoint directly in a browser returned 403 Forbidden. This was expected because normal browser navigation did not send the required x-api-key header. Once the API key and usage-plan associations were checked, the request succeeded in Postman.
8. Key Concepts Learned
- Function as a Service (FaaS): Run code in response to events without managing the underlying servers.
- AWS Lambda: Executes the function handler in response to an invocation.
- Amazon API Gateway: Exposes an API endpoint and routes requests to Lambda.
- Deployment stages: A REST API deployment must be associated with a stage, such as dev, to be invoked through its stage URL.
- API keys and usage plans: Help identify API consumers and apply request throttling and optional quotas.
- Postman: Sends requests with custom headers and verifies status codes and response bodies.
9. Answers to Project Questions
1. What is Function as a Service (FaaS)?
Function as a Service is a cloud computing model in which developers deploy functions that execute in response to events without provisioning or managing servers. AWS Lambda is an example of FaaS.
2. How many languages are supported by AWS Lambda?
Lambda supports multiple managed runtimes, including Node.js, Python, Java, .NET, Go, and Ruby, as well as custom runtimes. Runtime availability and versions change over time; consult the current AWS Lambda runtime documentation for the latest list.
3. What is the maximum memory allocated to an AWS Lambda function?
AWS Lambda supports memory configuration up to 10,240 MB (10 GB). Check the current AWS documentation if using this answer for an assessment.
4. How many ways are there to deploy a Lambda function?
Common deployment approaches include:
- AWS Management Console
- AWS Command Line Interface (AWS CLI)
- AWS SDKs
- AWS Serverless Application Model (AWS SAM)
- AWS CloudFormation
- Terraform
- CI/CD pipelines
These are common approaches, not a fixed official count.
5. Name some Lambda triggers other than API Gateway.
Examples include Amazon S3 events, Amazon SQS, Amazon SNS, Amazon DynamoDB Streams, Amazon EventBridge, and Amazon Kinesis.
6. How do you assign a role to Lambda?
Create or select an IAM execution role with only the permissions the function needs, then assign it under the Lambda function's Configuration → Permissions settings. The basic execution policy typically allows the function to write logs to CloudWatch Logs.
7. How can an API Gateway endpoint be secured?
Options include AWS IAM authorization, Amazon Cognito or another supported authorizer, Lambda authorizers, and API keys with usage plans. API keys alone should not be treated as strong user authentication.
8. How do you add API Gateway as a Lambda trigger?
Create an API Gateway API and method, configure the integration to invoke the Lambda function, ensure the required invocation permission is in place, and deploy the API to a stage.
10. Cleanup and Cost Notes
After the implementation and evidence capture, the API Gateway REST API, usage plan, API key, and Lambda function were deleted.

At the time of checking, the AWS Billing page showed an estimated total of USD $0.00 for October 2026. The bill was still pending, so the estimate could change as additional billing data arrived.

Deleting these project resources does not remove unrelated resources from the AWS account. Check AWS Billing and other services for any remaining resources or charges.
11. Possible Improvements
- Rebuild the API using AWS SAM or Terraform to demonstrate Infrastructure as Code (IaC).
- Add structured logging and error handling.
- Add an appropriate authorizer for stronger authentication where required.
- Configure CloudWatch alarms and request monitoring.
- Add automated tests and a CI/CD deployment pipeline.
12. References
- AWS Lambda — Getting Started
- Amazon API Gateway — Getting Started
- Tutorial: Build a Lambda function with API Gateway
- Control access to API Gateway APIs
- AWS Lambda runtimes
