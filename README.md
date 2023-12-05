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
### Deploying locally on minikube
To run this project locally, install it locally using minikube. To install minikube, follow [installing_minukube.md](minikube/installing_minukube.md). Once minikube is installed, use the below commands:

##### Start minikube and override of default cpu and memory
```
$ minikube start --memory=4096 --cpus =4
```
##### Create a dev namespace to align with Openshift. Switch context to the namespace
```
$ kubectl create -f adminnamespace-dev.yaml
$ kubectl config set-context --current --namespace=development
```

##### Check current context
```
$ kubectl config view
```

Output should show 
```
   namespace: development
    user: minikube
  name: minikube

```
##### To view all resources in a gui, kick off the minikube dashboard
minikube dashboard

## Helm chart sourced from

```
$ 
$ minikube start --memory=4096 --cpus =4
$ kubectl create -f adminnamespace-dev.yaml
$ 
```


	-* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
add a deployment for adding dev namespace - a1b9b0-dev
	kubectl create -f adminnamespace-dev.yaml
Switch to the dev namespace 
kubectl config set-context --current --namespace=<insert-namespace-name-here>
check namespaces
	kubectl get namespaces --show-labels


## Deploying to OpenShift

## Creating OpenShift ConfigMaps 

