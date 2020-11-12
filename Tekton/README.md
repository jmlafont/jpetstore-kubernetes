# Tekton CI/CD pipeline

pre-requisites:

git CLI:

oc CLI:

tkn CLI:

Openshift pipeline (tekton) Operator installed on an openshift cluster 

docker images are stored in two repositories:

- quay.io/jmlafont/jpetstore-web : application server
- quay.io/jmlafont/jpetstore-db : database

yaml file to deploy the application are in [../YAML](../YAML)



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
tkn pipeline start build-and-deploy-jpet
```



