# SAM Test Application

A test application to demo AWS Serverless Application Model, avoiding AppSync at all costs 
and using SAM only for CI/CD while avoiding proprietary bindings. This should demonstrate: 
1. A GraphQL Gateway with CORS and API keys
1. DynamoDB queries and updates
1. A public healthcheck endpoint
1. A scheduled function that executes a batch operation
1. Local testing


## Testing Locally

Unit tests can be run with `npm test`

You can invoke Lambda enpoints within a local Docker container with `sam local invoke`

Similarly you can run a local HTTP server with `sam local start-api`


## Deploying to AWS

To deploy this test app to your remote AWS stack:
1. `sam build`
1. `AWS_PROFILE=profile sam deploy`

As an alternative to the deploy you can perform a sync which will use the AWS Lambda, 
Amazon API Gateway, and AWS StepFunctions APIs to upload your code without performing 
a CloudFormation deployment, allowing you to quickly deploy changes to a dev environment.
This does cause drift in the CloudFormation stack and should only be used against 
a development stack... if at all. It seems to be more trouble than it is worth.
1. `AWS_PROFILE=profile sam sync --watch`


## License

This library is licensed under the MIT-0 License. See the LICENSE file.
