# Tekton CI/CD pipeline

## Introduction

In this workshop, you will build an application from its source files and deploy it to an OCP cluster using Openshift Pipeline.

- Source files are in the [../jpetstore](../jpetstore) subdirectory of this git repository
- yaml file to deploy the application are in [../YAML](../YAML) subdirectory
- pipeline definition is in [Pipeline.yaml](Pipeline.yaml) file

## Pre-requisites:

- a valid linux session
- git CLI installed
- oc CLI installed
- tkn CLI installed
- Openshift pipeline (tekton) Operator installed on an openshift cluster 
- two image repositories to store the images:
  - one to store the application server image 
  - second one to store the db server image 



## Workshop

clone the git repository on your linux session

```
git clone https://github.com/jmlafont/jpetstore-kubernetes.git
```

go into Tekton directory

```
cd jpetstore-kubernetes/Tekton
```

create a project:

```
oc new-project jpetstore-tekton-tuto
```

add a anyuid security context to the service account for the db to be able to start

```
oc adm policy add-scc-to-user anyuid -z default
```

have a look on the pipeline definition

- This pipeline uses the predefined ClusterTask **git-clone** to clone the source repository and store it in a workspace.
- Then it uses the ClusterTask **buildah** which build the application and the database images, according to the Dockerfiles found in the repository
- The last task deploy the application to the OCP cluster using the yaml files found in the repository

[optional] : edit the pipeline definition to change the parameters values

create the pipeline and tasks

```
oc apply -f Pipeline.yam
```

create  the persistent volume claim to define the persistent volume used to host the workspace

```
oc apply -f pvc.yaml
```

run the pipeline

```
tkn pipeline start build-and-deploy-jpet \
--workspace name=workspace,volumeClaimTemplateFile=pvc.yaml

```

Wait until the end of pipeline execution

![](./images/pipelinerun.jpg)

validate the deployment by finding the route and connect to the application

```
#oc get route
NAME                      HOST/PORT                       PATH   SERVICES   PORT   TERMINATION   WILDCARD
jpetstore-ingress-mf6zg   jpet.ocp2.iicparis.fr.ibm.com   /      web        9080                 None
```

