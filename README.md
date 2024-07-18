# Go Microservice Project

This project showcases a simple microservice developed using Go (Golang). It is containerized using Docker and is configured for deployment in a Kubernetes cluster. The microservice serves as a foundational template for building and deploying REST based Go applications in a cloud-native environment.

I deployed mine in an **OCI cluster** while working at **ORACLE**.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Building the Docker Image](#building-the-docker-image)
- [Deploying to Kubernetes](#deploying-to-kubernetes)
- [Running the Service](#running-the-service)
- [License](#license)

## Overview

This project demonstrates a sample REST based GOLANG microservice. The repository includes:

- Go source code for the microservice
- Dockerfile for building the Docker image
- Kubernetes service and deployment YAML files

## Prerequisites

Before you begin, ensure you have the following installed:

- [Go](https://golang.org/doc/install) (version 1.22.5 or higher)
- [Docker](https://docs.docker.com/get-docker/) or [Podman](https://podman.io/getting-started/installation)
- [Kubernetes](https://kubernetes.io/docs/setup/) cluster (e.g., Minikube, Kubernetes on Docker Desktop)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) command-line tool

## Setup

1. Clone the repository:

    ```sh
    git clone <REPO-NAME.git>
    cd <REPO-NAME>
    ```

2. Fetch the required Go dependencies:

    ```sh
    go mod tidy
    go mod download
    ```

## Building the Docker Image
Before starting with the commands below, make sure to change the directory where the Dockerfile is present.

1. Build the Docker image using Docker:

    ```sh
    docker build -t go-service:latest .
    ```

    Alternatively, using Podman (I used Podman to build the image due to restrictions on using Docker in my organisation):

    ```sh
    podman build -t go-service:latest .
    ```
    You can save the Docker image in a tar format to make it reusable.
    ```sh
    podman save -o <SAVED-IMAGE-NAME.tar> go-service:latest
    ```

## Deploying to Kubernetes

1. Apply the Kubernetes deployment and service YAML files:

    ```sh
    kubectl apply -f deployment.yaml (-n <namespace>  OPTIONAL) 
    kubectl apply -f service.yaml (-n <namespace>  OPTIONAL)
    ```

2. Verify the deployment:

    ```sh
    kubectl get deployments (-n <namespace>  OPTIONAL)
    kubectl get services (-n <namespace>  OPTIONAL)
    ```

## Running the Service

**Accessing the service locally:**
1. To access the service locally, you can port-forward the service to your local machine:

    ```sh
    kubectl port-forward svc/go-service 80:80 (-n <namespace>  OPTIONAL)
    ```
2. Open your web browser and navigate to `http://localhost:80` to access the service.
