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

In a few minutues, the pods should be in ready state. To check for any failures, get the pods in the dev namespace:
```
kubectl get pods --namespace a1b9b0-dev
```
To view the pod logs
```
kubectl logs <POD_NAME> --namespace a1b9b0-dev
```
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
To deploy to OpenShift, use OC commands and make sure Helm cli is installed on your local machine.
```
brew install helm
```

### Apply all the network policies and pod label policies under 'oc' folder:
Navigate to the 'oc' folder then:
```
oc apply -f .
```

#### Create default secrets
```
oc create secret generic airflow-mysql-secrets --from-literal=airflow-mysql-password=airflow_pass
oc create secret generic mysql-secrets --from-literal=openmetadata-mysql-password=openmetadata_password
oc create secret generic airflow-secrets --from-literal=openmetadata-airflow-password=admin
```
#### Deploy dependencies to OpenShift
Source: https://github.com/open-metadata/openmetadata-helm-charts/tree/main/charts/deps

Navigate to the 'deps' chart folder then:
```
helm install openmetadata-dependencies .
```
If you see the below error then get admin access to the dev namespace
Issues:  User "vikas.grover@gov.bc.ca" cannot get resource "roles" in API group "rbac.authorization.k8s.io" in the namespace "a1b9b0-dev"

#### Deploy OpenMetadata to OpenShift
Source: https://github.com/open-metadata/openmetadata-helm-charts/tree/main/charts/openmetadata

Once all the dependencies are running, navigate to the 'openmetadata' chart folder then:
```
helm install openmetadata .
```

Note: Always delete old PVC before re-deploying. Old volumes will break new pods.

#### Port forward OpenMetadata to view UI
```
oc port-forward service/openmetadata 8585:http
```

##  OpenSearch Dockerfile and Use of GHCR
OpenSearch requires a modified Dockerfile to work within the OpenShift restricted security context. The Dockerfile can be found under charts/opensearch-2.12.1/containers. The image is built automatically and pushed to the GHCR any time there is a push or PR to the **main** branch. 

Usage example: 
```sh
docker pull ghcr.io/bcgov/nr-openmetadata-opensearch:main
```

## Helm chart modifications
To review all Helm chart modifications (i.e. differences between the OpenMetadata default config and this config), search this repo for "DF-NOTE:" annotations.  
