## Table of contents
* [General info](#general-info)
* [Setup](#setup)

## General info
Minikube provides an easy way to spin up a single node Kubernetes cluster on a local machine. From https://minikube.sigs.k8s.io/docs/start/:
#What you’ll need
* 2 CPUs or more
* 2GB of free memory
* 20GB of free disk space
* Internet connection
* Container or virtual machine manager, such as: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation

## Setup
##### 1. Download the installer from https://storage.googleapis.com/minikube/releases/latest/minikube-installer.exe
##### 2. Start minikube and override of default cpu and memory
```
minikube start --memory=4096 --cpus =4
```
##### 3. Create a dev namespace to align with Openshift. Switch context to the namespace
```
kubectl create -f adminnamespace-dev.yaml
kubectl config set-context --current --namespace=development
```
##### 4. Check namespace in current context
```
kubectl config view --minify -o jsonpath='{..namespace}'
```
'a1b9b0-dev'
##### 5. To view all resources in a gui, kick off the minikube dashboard
minikube dashboard
