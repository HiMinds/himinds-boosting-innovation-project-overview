# Kubernetes Overview

In this document our aim is to give an overview of the Kubernetes engine and give a small summary of the features which we are going to use as a containerised enviroment management service for our IoT project.

There is more than one way to implement the environment as a service. We will list most of the possibilities related to the Kubernetes engine so we can ellaborate on what should be the inplementation for our service?

## What is Kubernetes?

Kubernetes' aim is to run a containerised service in a distributed high availability environment.

To know more about Kubernetes as a product read the official website:
https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/

## Understanding Kubernetes

Kubernetes as a service can be implemented in different ways however has to fulfill the following design criterias:
* pods: a group of containers which run as one homogenous service on one of the nodes (shared namespace, shared volumes, shared network, shared resources)
* node: a computer which can run the pod(s)

So all the information which is needed to run the pods in one of the nodes and replicate the service to another host is stored and managed within the Kubernetes engine services inplementation.

### Bare minimum

If you want to install and manage Kubernetes:
* docker-engine: for the virtualisation, containerisation, resource management, volume and network management
* kubelet: the node manager
* kubeadm: create Kubernetes clusters
* kubectl: command line interface to interact to the Kubernetes engine
* kubernetes-cni: kubernetes netwrok interface 

If you just want to connect to a kubernetes service install:
* kubectl
* Kubernetes has a build in API service which you can use to connect and change the Kubernetes service configuration

You can create manifest files to set up the Kubernetes containerised service and configure the environment and set up the service through the api.

### Helm package manager

Kubernetes runs containers. It is possible to use a package manager created for Kubernetes called Helm. It uses manifest templates and uses the images pulled down from the repository server.

### Monitoring and logging

You can use Liveness and Readiness Probes to monitor the service health and restart the service if it is necessary.

As a general solution you can use:
* Prometheus to monitor the Kubernetes service.
* EFK (Elasticksearch, Fluentd and Kibana).

The different cloud providers have their own monitoring solutions which might support Kubernetes monitoring and logging.

### Basics of workload management

You can execute all the service management on a Kubernetes by the kubectl command line.
If you want to store as infrastructure as code you can use manifest (yaml) files. That's what we will do during our project.
You can create:
* Objects
* Pods
* Environment
* Roles
... and many more. For example you can set up targets as urls so you can get or write your settings directly to the net!
Also as a result you can manage deployments from git commits.

## Kubernetes development envinronment

If you want to try out Kubernetes or learn it is easy to set up a local development environment with Kubernetes. You need a Linux desktop and minikube. 

### Basic components

* hypervisor (e.g VirtualBox, KVM)

Check the provider's webpage for installation steps.

* Docker engine

Check the Docker webpage how to install it.

* minikube cli

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v1.2.0/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
minikube version
```

* kubectl cli

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
which kubectl
```

### minikube

To start up minikube:
```
minikube start
```
But you can assign more resources at the creation of the cluster from the command line:
```
minikube start --cpus=4 --memory=4000 
```

To start the api proxy:
```
kubectl proxy --port=8080 &
curl http://localhost:8080/api/
```

To view the services on a dashboard:
```
minikube dashboard
```

### Google Kubernetes

Our IoT service will run on the Google Cloud platform. Kubernetes has been designed by Google and the Google Cloud Platform has a build in Kubernetes Engine. You can find more information here: 
https://cloud.google.com/kubernetes-engine/

### Terraform provider

Terraform has providers both for cloud services both for Kubernetes clusters. The Kubernetes provider uses the K8S Go library which is packaged with Terraform. So basically from Terraform configuration you can set up and configure the Kubernetes service as infrastructure as code.

* You can find more information how to set up a service with the Terraform Kubernetes provider here. https://www.terraform.io/docs/providers/kubernetes/index.html

* To create the Kubernetes container enginee can use the Google cloud provider. You can reserve the resources and design the infrastructure here. 

* Terraform has null providers which allows you to run command lines like kubectl commands. 


### Kubernetes workload configuration best practices

### Kubernetes environment configuration

### Kubernetes service configuration

### Automated deployment management with Kubernetes

## Useful links
