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

## Problem Statements: FProblem Statements

[Problem Statements](problems): Problem Statements **HOW TO**


## Solution

![architecture_design](docs/design.svg)

The diagram describes the picturial description of my solution:

## Project requirements
It is assume that this demo is for learning purpose, so best production and security practices are not fully considered:
- I will deploy 11 microservices with helmfile
- Frontend service - entrypoint for the application that is accessible externally
- Redis - 3rd party service that store data
- All the microservices images, env, port are based on the original repo from gcr sample
- I use a single namespace
- All the microservice commmunicate using API call

## Demo
[Prepare kubernetes environment and get helm install](#prepare-k8s-env-and-get-helm-install)
[Create a common chart for 10 microservices](#create-a-common-chart-for-10-microservices)
![screenshot_helm_create](docs/helm-create.png)


[Set default and actual value for each microservices](#set-value-for-each-microservices)

  - Need to validate if all the values define is correct up till this point
  Run the command; helm template -f email-service-value.yaml common-chart & helm lint -f email-service-value.yaml common-chart
  - Then, deploy one of the service to check if this work
  Run the command; helm install common-chart ./helm-charts/common-chart/ & helm list
[Create redis helm chart](#create-redis-helm-chart)
[Deploy microservice to kubernetes with helmfile](#deploy-microservice-to-kubernetes-with-helmfile)

## Lesson Learnt