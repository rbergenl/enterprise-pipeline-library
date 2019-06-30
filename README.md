Enterprise Pipeline Library
---

sendTriggerIntegration      <- key <- GitHub (Hook) -  provision a build agent in response to demand, e.g. a PR request, or a push to master in your GitHub repo.
receiveTriggerIntegration
checkoutSCM                 -> key -> Github
scanSonar                   -> key -> SonarQube
gitRelease                  -> key -> Github
npmPublish                  -> key -> Nexus
uploadAWS                   -> key -> AWS Dev

receiveTriggerDeployment
deployAWSDev                -> key -> AWS Dev
deployAWSTest               -> key -> AWS Test
deployAWSProd               -> key -> AWS Prod

# Getting Started
- Initial Master configuration: jenkins.config.json
- Docker: build
- Flows: feature, develop and master
- Maven: build, test
- NPM: install, test, build, publish
- Scans: fortify (security of ...), nexus (security of dependencies), owasp (security of ...), sonar (code quality), twistlock (security of docker image), restassured (testing of api)

# Folder Structure
    .
    ├── reference-deployment-pipeline
    |   ├── cdn                 # A pipeline that deploys static files to a AWS Content Delivery Network
    |   ├── ecs                 # A pipeline that deploys a container to AWS Elastic Container Service
    ├── reference-integration-pipeline
    |   ├── docker-java         # A pipeline that ends up with publishing a Java runtime image to a Docker registry
    |   ├── docker-node         # A pipeline that ends up with publishing a Node runtime image to a Docker registry
    |   └── npm                 # A pipeline that ends up with publishing a package to a NPM registry
    └── var                     # Groovy files with commands for each step in a pipeline

> Folders with an * are not source code but contains generated files

# Continuous Integration
- Blog: https://jenkins.io/blog/2018/10/16/custom-war-packager/#jenkinsfile-runner-packaging
- Usage: https://github.com/jenkinsci/jenkinsfile-runner/blob/master/DOCKER.md
- `docker run --rm -v $PWD/demo/Jenkinsfile:/workspace/Jenkinsfile onenashev/cwp-jenkinsfile-runner-demo`
- `docker build -t rbergenl/jenkinsfile-runner:latest --build-arg JENKINS_VERSION=2.121.1 .`
- `docker run --rm -v ${PWD}:/workspace rbergenl/jenkinsfile-runner:latest`

## Permissions
- Give Jenkins permissions to the SCM repository (using SSH keys)
- Give Jenkins permissions to SonarQube (username/password)
- Give Jenkins permissions to publish to Nexus (npm add user username:password)
- Give Jenkins permissions to publish to AWS S3 (externalID and assumeRole)

# Continuous Deployment
The shared templates to create a pipeline are host in a S3 bucket.
This template can be referenced as a nested stack into a Master template.

References are the templates to be used inside other projects

Two deployment pipelines are available:
- Deploy a Docker container into Elastic Container Service - Fargate.
- Deploy a Content Delivery Network to serve static files.

CloudFormation templates to create an infrastructure stack on AWS

## Permissions
- Give the AWS Production account a cloudformation role which trusts the AWS Development account
- Give the AWS Development account permission to pull from Nexus (username:password)

# Contributing
- Read the `CONTRIBUTING.md` file for the guidelines.
