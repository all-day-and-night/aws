Serverless API Gateway
=================

> client <-rest api-> API Gateway <-proxy Request-> Lambda <-CRUD-> DynamoDB

# Integration

> Lambda Function

> HTTP

> AWS Service

# Endpoint Types

- Edge-Optimized (default) : For Global clients

> through CloudFront Edge locations

> the api Gateway still lives in only one region

- Regional

> For clients within the same region

- Private
> Can only access from VPC using an interface VPC endpoint

# Security 

- User Authentication through

> IAM Roles
> Cognito
> Custom Authorizer(your own code)

- Custom Domain Name HTTPS

> if using Edge-Optimized endpoint, then the certificate must be in us-east-1
> if using Reginal endpoint, the certificate must be in the API Gateway region
> Must setup CName or A-alias record in Route 53