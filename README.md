# microservices-demo
How I implemented the sample cloud-native application with 11 microservices showcasing Kubernetes and managed by helm. Original repo; https://github.com/GoogleCloudPlatform/microservices-demo


## Table of contents
<!-- TOC -->
* [A journey into microservice](#a-journey-into-microservice)
  * [Problem Statements](#problem-Statements)
  * [Solution](#solution)
  * [Project requirements](#project-requirements)
  * [Demo](#demo)
    * [Prepare kubernetes environment and get helm install](#prepare-k8s-env-and-get-helm-install)
    * [Create a common chart for 10 microservice](#create-a-common-chart-for-10-microservice)
    * [Create actual value for each microservice](#create-actual-value-for-each-microservice)
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
- I will deploy 11 microservice with helmfile
- Frontend service - entrypoint for the application that is accessible externally
- Redis - 3rd party service that store data
- All the microservice images, env, port are based on the original repo from gcr sample
- I use a single namespace
- All the microservice commmunicate using API call