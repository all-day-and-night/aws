how to use docker in aws?
===============

# Docker

> software development platform to deploy apps\

# Docker containers Management on AWS

1. Amazone Elastic container Service(ECS)

> Amazoe's own container platform

2. Amazone Elastic Kubernetes Service(EKS)

> Amazon's managed Kubernetes(open source)

3. AWS Fargate

> Amazon's onw Serverless container platform

> Works with ECS and with EKS

4. Amazon ECR

> store container images

# ECS

> ECS Cluster는 Ec2 instances를 먼저 provisioning 한 후 infrastructure를 구축한 뒤 container를 올린다.

> 

> FSx for Lustre is not supported

> Amazon S3 cannot boe mounted as a file system

* Auto Scaling

> CPU utilizaton + Memory Utilization + ALB Request Count Per Target

* Target Tracking

* Step Scaling

* Scheduled Scaling 




## ECR


```
# login Command 
$ aws ecr get-login-password --region "region" | docker login --username AWS -- password-stdin "aws_account_id".dkr.ecr."region".amazonaws.com

# Docker Push
$ docker push "aws_account_id".dkr.ecr."region".amazonaws.com/demo:latest

# Docker pull
$ docker pull "aws_account_id".dkr.ecr."region".amazonaws.com/demo:latest

```