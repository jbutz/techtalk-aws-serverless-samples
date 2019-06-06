# AWS Serverless Application with CI/CD Example

This repository contains working code samples for a talk on AWS, Serverless, and CI/CD. The `api/` directory contains an [AWS SAM](https://github.com/awslabs/serverless-application-model) app. The `app/` directory contains an app created with [Create React App](https://github.com/facebook/create-react-app). Both are very basic "hello world" type applications.

## Installation

To use these examples you will need an [AWS](https://aws.amazon.com) account. Having the [AWS CLI](https://aws.amazon.com/cli/) installed and configured for that account will also make things easier.

You will also need this code to be located in a GitHub repository in order to deploy it with the current CI/CD pipeline. You will also need a GitHub Personal Access Token, it should have `repo` permissions and `admin:repo_hook` permissions.

In order to deploy the SAM app and the React app you need to deploy the CI/CD pipeline first. To do that you can run the following command. You will need to update the following:
- `RepositoryName` to match your GitHub repo's name
- `GitHubOwner` to match the user or organization account the repo belongs to
- `GitHubOAuthToken` to match the Personal Access Token the pipeline should use
- `AppName` to the name you want to use for your application. This cannot match the `stack-name` value
- `SecretValue` to some semi-random value to help secure the webhook that triggers the pipeline

```bash
aws cloudformation deploy \
    --template-file cfn-deployment.yml \
    --stack-name techtalk-deploy-example \
    --capabilities CAPABILITY_NAMED_IAM \
    --parameter-overrides RepositoryName=techtalk-aws-serverless-samples GitHubOwner=jbutz GitHubOAuthToken=1234567890abcdef AppName=techtalk-example SecretValue=b9204ab70e67593283
```

After running that command a new CloudFormation template should have been created and it should have deployed a CodePipeline, which will pull the GitHub repo and deploy the code.

## Contributing
Pull requests are welcome, but this code is mainly for use as an example. As such it is not intended for production. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
