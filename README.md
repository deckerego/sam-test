# SAM Test Application

A test application to demo AWS Serverless Application Model, avoiding AppSync at all costs 
and using SAM only for CI/CD while avoiding proprietary bindings. This should demonstrate: 
1. A GraphQL Gateway with CORS and API keys
1. DynamoDB queries and updates
1. A public healthcheck endpoint
1. A scheduled function that executes a batch operation
1. Local testing


## Testing Locally

Ipsum sed


## Deploying to AWS

To deploy this test app to your remote AWS stack:

1. `sam build`
1. `sam deploy --guided`


## License

This library is licensed under the MIT-0 License. See the LICENSE file.
