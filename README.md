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
### Deploying locally on minikube using Helm chart
To install minikube, follow [installing_minukube.md](minikube/installing_minukube.md). Once minikube is installed, use the below commands (the installation uses Helm charts for deploying to k8s)

#### Helm chart source: https://helm.open-metadata.org/
#### Create Kubernetes Secrets required for Helm Charts
```
kubectl create secret generic mysql-secrets --from-literal=openmetadata-mysql-password=openmetadata_password
kubectl create secret generic airflow-secrets --from-literal=openmetadata-airflow-password=admin
kubectl create secret generic airflow-mysql-secrets --from-literal=airflow-mysql-password=airflow_pass
```
#### Add Helm Repository for Local Deployment
```
helm repo add open-metadata https://helm.open-metadata.org/
```
To verify, run ```helm repo list``` to ensure the OpenMetadata repository was added.

#### Install OpenMetadata Dependencies Helm Chart
```
helm install openmetadata-dependencies open-metadata/openmetadata-dependencies
```
Run ```kubectl get pods``` to check whether all the pods for the dependencies are running. You should get a result similar to below.

Helm Chart for OpenMetadata Dependencies uses the following helm charts:
Bitnami MySQL (helm chart version 9.7.1)
ElasticSearch (helm chart version 7.16.3)
Airflow (helm chart version 8.6.1)

#### Install OpenMetadata Helm Chart
Deploy OpenMetadata Application by running the following command -
```
helm install openmetadata open-metadata/openmetadata
```
#### Port Forward OpenMetadata Kubernetes Service to view UI
```
kubectl port-forward service/openmetadata 8585:http
```
The above command will port forward traffic from local machine port 8585 to a named port of OpenMetadata kubernetes service http.
Browse the Application with url http://localhost:8585 from your Browser. The default login credentials are admin:admin to log into OpenMetadata Application.

#### Cleanup
Use the below command to uninstall OpenMetadata Helm Charts Release.
```
helm uninstall openmetadata
helm uninstall openmetadata-dependencies
```

## Deploying to OpenShift

## Creating OpenShift ConfigMaps 

