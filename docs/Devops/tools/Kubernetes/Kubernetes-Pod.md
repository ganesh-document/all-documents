## **Kubernetes - Pod**

A pod is a collection of containers and its storage inside a node of a Kubernetes cluster. It is possible to create a pod with multiple containers inside it.

For example, keeping a database container and data container in the same pod.

**Types of Pod**

There are two types of Pods −

  1. Single container pod
  2. Multi container pod

**Single Container Pod**

They can be simply created with the kubctl run command, where you have a defined image on the Docker registry which we will pull while creating a pod.

```
$ kubectl run <name of pod> --image=<name of the image from registry>
```

**Example −** We will create a pod with a tomcat image which is available on the Docker hub.

```
$ kubectl run tomcat --image = tomcat:8.0
```

This can also be done by creating the yaml file and then running the kubectl create command.

```
apiVersion: v1
kind: Pod
metadata:
   name: Tomcat
spec:
   containers:
   - name: Tomcat
    image: tomcat: 8.0
    ports:
containerPort: 7500
   imagePullPolicy: Always
```

Once the above yaml file is created, we will save the file with the name of tomcat.yml and run the create command to run the document.

```
$ kubectl create –f tomcat.yml
```

It will create a pod with the name of tomcat. We can use the describe command along with kubectl to describe the pod.

**Multi Container Pod**

Multi container pods are created using yaml mail with the definition of the containers.

```
apiVersion: v1
kind: Pod
metadata:
   name: Tomcat
spec:
   containers:
   - name: Tomcat
    image: tomcat: 8.0
    ports:
containerPort: 7500
   imagePullPolicy: Always
   -name: Database
   Image: mongoDB
   Ports:
containerPort: 7501
   imagePullPolicy: Always
```

In the above code, we have created one pod with two containers inside it, one for tomcat and the other for MongoDB.

