# AWS SAM CodeBuild CI ![Build Status](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoieTUyMUdIS2RLYWRpZVRSOVozWkI5WjV0c2tlTnh0elBVTGF6OWNXVkM0TkFhSkpOSG0ySzVyMVQzcmdOWG5XNEl4UHY1MzJYdm1lbk56MXVOcmE0eFdJPSIsIml2UGFyYW1ldGVyU3BlYyI6ImRIN20zWitGRVRaRUJ1RzciLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)

This serverless app sets up an AWS CodeBuild Project as a CI solution for a GitHub-based SAM project. Once setup, every time you push to a branch in your GitHub repository, CodeBuild will kick off a build verifying your latest changes. This can be used as an automated check on pull requests (PRs) to your GitHub repo. This app also uses [github-codebuild-logs](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:277187709615:applications~github-codebuild-logs) app to allow anyone to view the build logs from AWS CodeBuild Project in pull requests.

## Installation

1. [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and login
1. Create a GitHub OAuth token (see instructions below).
1. Connect AWS CodeBuild to your GitHub account via the AWS Console (see instructions below).
1. Go to this app's page on the [Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:646794253159:applications~aws-sam-codebuild-ci) and click "Deploy"
1. Provide the required app parameters and click "Deploy"

### Creating a GitHub OAuth token

General instructions for creating a GitHub OAuth token can be found [here](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/). When you get to the scopes/permissions page, you should select the "repo" and "admin:repo_hook" scopes, which will automatically select all permissions under those two scopes.

![GitHub OAuth Token Permissions](https://github.com/awslabs/aws-sam-codebuild-ci/raw/master/images/github-token-permissions.png)

### Connect AWS CodeBuild to your GitHub account

Connecting AWS CodeBuild for your account to your GitHub account is a manual step that only needs to be performed once for your account in a given region. To do this, follow these steps:

1. Login to the [AWS CodeBuild Console](https://console.aws.amazon.com/codesuite/codebuild/home).
1. Switch to the region to which you're going to deploy the CI app.
1. Click "Create Project".
1. Scroll down to the "Source" section.
1. Select "GitHub" as the source provider.
1. Click "Connect to GitHub".
1. AWS CodeBuild is now connected to your GitHub account. You do not need to complete the Create Project flow and can close the page and return to the installation steps.

**Note:** If you do not see the "Connect to GitHub" button in step 6 and instead see options to select one of your GitHub repositories, AWS CodeBuild is already connected to your GitHub account and no further action is necessary.

## Parameters

The app has the following parameters:

1. `GitHubOwner` (required) - GitHub username owning the repo.
1. `GitHubRepo` (required) - GitHub repo name (just the name, not the full URL).
1. `GitHubOAuthToken` (required) - OAuth token used by AWS CodeBuild to connect to GitHub.
1. `ComputeType` (optional) - AWS CodeBuild project compute type to use. See [Create a Build Project (AWS CLI)] (https://docs.aws.amazon.com/codebuild/latest/userguide/create-project.html#create-project-cli) for details. Default: BUILD_GENERAL1_SMALL
1. `EnvironmentType` (optional) - Environment type used by AWS CodeBuild. See [Create a Build Project (AWS CLI)] (https://docs.aws.amazon.com/codebuild/latest/userguide/create-project.html#create-project-cli) for details. Default: LINUX_CONTAINER

## App Outputs

1. `CodeBuildProjectName` - Name of the CodeBuild project.
1. `CodeBuildProjectArn` - ARN of the CodeBuild project.
1. `ArtifactsBucketName` - Name of the Artifacts S3 bucket used by CodeBuild.
1. `ArtifactsBucketArn` - ARN of the Artifacts S3 bucket used by CodeBuild.

## License Summary

This sample code is made available under the MIT-0 license. See the LICENSE file.
