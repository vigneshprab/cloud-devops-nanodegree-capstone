## Capstone Project

In this project you will apply the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These include:

* Working in AWS
* Using Jenkins to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters
* Building Kubernetes clusters
* Building Docker containers in pipelines

---
### Setting your AWS infrastructure

Execute cloudformation scripts inside infra/ folder:

    sh ./create.sh DevOpsCapstone eks_network.yml infra-params.json
    
Note: Creation of EKS cluster takes 15 minutes

### Setting your pipeline for lint, build and publish your docker image

Pipeline Creation: Add `Jenkinsfile` in jenkins, and run the pipeline. Docker Credentials needs to be  configured in Jenkins.

### Blue Green deployment configuration is setting in Kubernetes using Controllers and Service

1) Apply blue controller inside application/blue folder
    
    `kubectl apply -f blue-controller.json`
    
2) Apply green controller inside application/green folder
    
    `kubectl apply -f green-controller.json`
    
3) Deploy service in application/ folder

    `kubectl apply -f blue-green-service.json`
    
   Then you can check the application deployed in your browser
    
4) For doing a blue-green deployment update the section to **green** in blue-green-service.json file:


    "selector":{
          "app":"blue" 
        },

5) Deploy again the service

    `kubectl apply -f blue-green-service.json`
    
---
