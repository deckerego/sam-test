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

You can invoke Lambda enpoints within a local Docker container with `sam local invoke`. 
Sample events are provided in the `events/` directory - e.g.:
```
sam-test % sam local invoke getAllItemsFunction --event events/event-get-all-items.json
```

and local HTTP server can be launched to field requests via `sam local start-api`.

If you are running Docker via Docker Desktop, see the entry 
[Local Errors with Docker Desktop](#local-errors-with-docker-desktop) below
to properly set `DOCKER_HOST` to the current context.


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


## Local Errors with Docker Desktop

Recent builds of Docker Desktop may set the `DOCKER_HOST` environment variable to be something
other than the current context
(see [SAM CLI Issue #4329](https://github.com/aws/aws-sam-cli/issues/4329#issuecomment-1289588827)).
You can test for this issue by running `docker context ls` and confirming that your current context 
is different than the `DOCKER_HOST` context:
```
sam-test % docker context ls                                                           
NAME              DESCRIPTION                               DOCKER ENDPOINT                                   ERROR
default           Current DOCKER_HOST based configuration   unix:///var/run/docker.sock                       
desktop-linux *   Docker Desktop                            unix:///Users/username/.docker/run/docker.sock   
```

The easiest way to deal with this is to set the `DOCKER_HOST` environment variable yourself using:
```
export DOCKER_HOST=$(docker context inspect | jq -r '.[0].Endpoints.docker.Host')
```

This can be added to your `.zprofile` shell config on MacOS, or to your `.profile` for Bash.
