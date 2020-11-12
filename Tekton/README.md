# Tekton CI/CD pipeline

## Introduction

In this workshop, you will build an application from its source files and deploy it to an OCP cluster using Openshift Pipeline.

- Source files are in the [../jpetstore](../jpetstore) subdirectory of this git repository
- yaml file to deploy the application are in [../YAML](../YAML) subdirectory
- pipeline definition is in Tekton/Pipeline.yaml file

## Pre-requisites:

- a valid linux session
- git CLI installed
- oc CLI installed
- tkn CLI installed
- Openshift pipeline (tekton) Operator installed on an openshift cluster 
- two image repositories:
  - one to store the application server image  (default :quay.io/jmlafont/jpetstore-web to be replaced by your own repository)
  - second one to store the db server image  (default :quay.io/jmlafont/jpetstore-db to be replaced by your own repository)



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
oc new-project jpetsore-tekton-tuto
```

create the pipeline and tasks

```
oc apply -f Pipeline.yam
```

run the pipeline

```
tkn pipeline start build-and-deploy-jpet \
--workspace name=workspace,volumeClaimTemplateFile=pvc.yaml

```

add a security context for database

```
oc adm policy add-scc-to-user anyuid -z default
```

