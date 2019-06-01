Enterprise Pipeline Library
---

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

# Continuous Deployment
The shared templates to create a pipeline are host in a S3 bucket.
This template can be referenced as a nested stack into a Master template.

References are the templates to be used inside other projects

Two deployment pipelines are available:
- Deploy a Docker container into Elastic Container Service - Fargate.
- Deploy a Content Delivery Network to serve static files.

CloudFormation templates to create an infrastructure stack on AWS


# Contributing
- Read the `CONTRIBUTING.md` file for the guidelines.
