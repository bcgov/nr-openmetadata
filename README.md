## Table of contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Setup](#setup)

## General info
As of 2023-12-05, this project is simple demonstration of running OpenMetadata in Openshift. 
	
## Technologies
Project is created with:
* Docker
* Minikube
* Openshift
* OpenMetadata
	
## Setup
To run this project locally, install it locally using minikube. To install minikube, follow installing_minukube.md. Once minikube is installed, use the below commands:

```
$ minikube start --memory=4096 --cpus =4
$ kubectl create -f adminnamespace-dev.yaml
$ 
```

## Helm chart sourced from

## Deploying locally on minikube
minikube start --memory=4096 --cpus =4
	-* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
add a deployment for adding dev namespace - a1b9b0-dev
	kubectl create -f adminnamespace-dev.yaml

check namespaces
	kubectl get namespaces --show-labels


## Deploying to OpenShift

## Creating OpenShift ConfigMaps 

