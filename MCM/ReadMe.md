# Creation et deploiement de l'appli JPetStore depuis MCM

- creer les namespaces (jpet-definition,jpet-project ) sur le hub

- creeer les ressources:

```
/home/jpetstore/jpetstore-kubernetes/MCM
[root@niceay MCM]# oc apply -f deployable.yaml
deployable.app.ibm.com/jpetstore-deployment created
deployable.app.ibm.com/jpetstoredb-deployment created
deployable.app.ibm.com/jpetstore-service-np created
deployable.app.ibm.com/jpetstore-dbservice created
deployable.app.ibm.com/jpetstore-route created
```

```
[root@niceay MCM]# oc apply -f channel.yaml
channel.app.ibm.com/jpetstore-devchan created
```

```
[root@niceay MCM]# oc apply -f subscription-web.yaml
subscription.app.ibm.com/jpetstore created
[root@niceay MCM]# oc apply -f subscription-db.yaml
subscription.app.ibm.com/jpetstore-db created
```

```
[root@niceay MCM]# oc apply -f subscription-db.yaml
subscription.app.ibm.com/jpetstore-db configured
[root@niceay MCM]# oc apply -f subscription-web.yaml
subscription.app.ibm.com/jpetstore configured
```

```
[root@niceay MCM]# oc apply -f placementrule-db.yaml
placementrule.app.ibm.com/jpetstore-placement-db created
[root@niceay MCM]# oc apply -f placementrule-web.yaml
placementrule.app.ibm.com/jpetstore-placement created
```

```
[root@niceay MCM]# oc apply -f application.yaml
application.app.k8s.io/jpetstore created
```



Ces actions créent de CR sur le hub:

![image-20201014135329367](image-20201014135329367.png)

​	

![image-20201014135755056](image-20201014135755056.png)



L'appli devient visible depuis MCM

![image-20201014135913599](image-20201014135913599.png)



Puis, une fois le cluster labellé conformement aux placement rules et le namespace destination créé sur la cible, l'application et automatiquement déployée:

![image-20201014161250064](image-20201014161250064.png)



Pour tester:

- recuperer le port assigné au service,

![image-20201014192204143](image-20201014192204143.png)

- récupérer l'adresse externe d'un noeud du cluster cible

![image-20201014192455170](image-20201014192455170.png)

![img](SNAGHTML223f5b5.PNG)

![img](SNAGHTML224af9f.PNG)

- construire l'URL 

![image-20201014161427643](image-20201014161427643.png)

