# microservices-demo
How I implemented the sample cloud-native application with 11 microservices showcasing Kubernetes and managed by helm. Original repo; https://github.com/GoogleCloudPlatform/microservices-demo


## Table of contents
<!-- TOC -->
* [A journey into microservice](#a-journey-into-microservices)
  * [Problem Statements](#problem-Statements)
  * [Solution](#solution)
  * [Project requirements](#project-requirements)
  * [Demo](#demo)
    * [Prepare kubernetes environment and get helm install](#prepare-k8s-env-and-get-helm-install)
    * [Create a common chart for 10 microservices](#create-a-common-chart-for-10-microservices)
    * [Set default and actual value for each microservices](#set-value-for-each-microservices)
    * [Create redis helm chart](#create-redis-helm-chart)
    * [Deploy microservice to kubernetes with helmfile](#deploy-microservice-to-kubernetes-with-helmfile)
  * [Lesson Learnt](#Lessons)
<!-- TOC -->

## Problem Statements: Problem Statements

[Problem Statements](problems): Problem Statements
How can I deploy and manage existing microservices in a kubernetes cluster?

## Solution
![architecture_design](docs/design.svg)
The diagram describes my solution in picture:

## Project requirements
It is assume that this demo is for learning purpose, so best production and security practices are not fully considered:
- I will deploy 11 microservices with helmfile
- Frontend service - entrypoint for the application that is accessible externally
- Redis - 3rd party service that store data
- All the microservices images, env, port are based on the original repo from gcr sample
- I use a single namespace
- All the microservices commmunicate using API call

## Demo
If you want to follow along this demo, fork the repo. Clone the repo into your local machine. Change into the directory where it was clone to.
[Prepare kubernetes environment and get helm install](#prepare-k8s-env-and-get-helm-install)
  - Set up minikube on your machine and get helm install. 
  - Pretty simple process; check out the steps from official doc at https://kubernetes.io/docs/tasks/tools/ and https://helm.sh/docs/intro/install/

[Create a common chart for 10 microservices](#create-a-common-chart-for-10-microservices)
  - I created a common chart for the 10 microservices of the application and later a chart for the 3rd party service, in this case redis. Run the command; ```helm create common-chart```
  - At the creation, the chart will contain the following;
    - chart folder - chart dependencies
    - template folder - dir where actual k8s YAML files created, blueprint
    - Chart.yaml - meta info about the chart
    - values.yaml - default values for the template files
    - .helmignore - files need not include in the helm chart
![screenshot_helm_create](docs/helm-create.png)


[Set default and actual value for each microservices](#set-value-for-each-microservices)

  - Need to validate if all the values define is correct up till this point.
  Run the command; ```helm template -f email-service-value.yaml common-chart``` & ```helm lint -f email-service-value.yaml common-chart```
  - Then, deploy one of the service to check if this work.
  Run the command; ```helm install common-chart ./helm-charts/common-chart/``` & ```helm list```

[Create redis helm chart](#create-redis-helm-chart)

[Deploy microservice to kubernetes with helmfile](#deploy-microservice-to-kubernetes-with-helmfile)

## Lesson Learnt