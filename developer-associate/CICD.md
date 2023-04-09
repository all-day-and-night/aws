CI / CD
===========


> automating the deploymebt we've done so far while adding increased safety

# what we learn

1. AWS Code Commit : Storing our code
2. AWS CodePipeline : automating out pipeline from code to Elastic BeanStalk
3. AWS CodeBuild : building and testing our code
4. AWS CodeDeploy : Deploying the code to EC2 instances(not Elastic BeanStalk)
5. AWS CodeStar : manage software development activities in one place
6. AWS CodeArtifact : store, publish, and share software packages

# CI

> Continuous Integration(CI)

* repository: github, bitbucket

* test / build server checks teh code asap it's pushed (CodeBuild, Jenkins)

* just developers push codes


# CD

> Continuous Delivery

* CodeDeploy, Jenkins


# CodeCommit

* Version Control

* Git 사용

* online repository에 기반하여 로컬에서 동기화 하여 작업 가능

* 동시 개발 가능

* version controll을 통해 back up 및 roll back 가능

- Github, Gitlab, BitBucket

- private git repository
- No size limit
- Fully managed, highly available
- Code only in AWS Cloud account -> increased security and compliance
- integrated with Jenkins, AWS Code Build, and other CI Tools

* Security

- Authentication
 * SSH keys
 * HTTPS

- Authorization
 * IAM policies to manage user/rols permissions to repositories

- Encryption
 * Automatically encrypted at rest using AWS KMS

- Cross-account Access
 * Do not share your ssh keys or your AWS credentials



# Code Pipeline

> orchestrate your CICD

## workflow

1. Source - CodeCommit, ECR, S3, Bitbucket, Github
2. Build - CodeBuild, Jenkins, CloudBees, TeamCity
3. Test - CodeBuild, AWS Device Rarm, 3rd party tools...
4. Deploy - CodeDeploy, Elastic BeanStalk, CloudFormation, ECS, S3

* Consist of Stages:
 - Each stage can have sequential actions and/or parallel actions
 - Build -> test -> Deploy -> Loading test 

## Trouble shooting

- For codePipeline pipeline/action/stage Execution state changes
- Use Cloud Watch Events (Amazon EventBridge)

# AWS CodeBuild

> Code file "buildspec.yml"(exists in root directory) or insert manually in Console

## buildspec.yml

> must be at the root of your code

* env - define environment variables
    - variables : plaintext variables
    - parameter-store: variables stored in SSM Parameter Store
    - secrets-manager : variables stored in AWS Secrets Manager

* phases - specify commands to run:
    - install : install dependencies you may need for your build
    - pre_build : final commands to execute before build
    - build : actual build commands
    - post_build : finishing touches

* artifacts - what to upload to S3(encrypted with KMS)

* cache - files to cache(usually dependencies) to S3 for future build speedup


# AWS CodeDeploy

> "appspec.yml" in root of your code

## Primary Components

1. Application - unique name functions as a container(revision, deployment configuration)

2. Compute Platform - EC2/On-Premises, AWS Lambda or Amazon ECS

3. Deployment Configuration - a set of deployment rules for success/failure
    - EC2/On-premises: specify the minimum number of healthy instances for the deployments
    - AWS Lambda or Amazon ECS: specify how traffic is routed to your updated versions

4. Deployment Group
    - group of tagged EC2 instances(allows to deploy gradually or dev, test, prod...)

5. Deployment Type: method used to deploy the application to a Deployment Group
    - In-place Deployment: support EC2/On-premises
    - Blue/Green Deployment: support EC2 instances only, AWS Lambda, and Amazon ECS

6. IAM Instance Profile
    - give EC2 instances the permissions to access both S3 / github

7. Application Revision : application code + appspec.yml file

8. Service Role : an IAM Role for CodeDeploy to perform operations on EC2 instances, ASGs, ELBs...

9. Target Revision - the most recent revision that you want to deploy to a Deployment Group


# CodeStar 

* integrated solution that groups 
    - github, codecommit, codebuild, codedeploy, cloudFormation, codepipeline, cloudwatch

