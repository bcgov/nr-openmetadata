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
1. Download the installer from https://storage.googleapis.com/minikube/releases/latest/minikube-installer.exe
2. minikube start
3. kubectl get po -A
4. minikube stop
5. minikube delete --all