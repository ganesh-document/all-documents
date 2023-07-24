## **Kubernetes - Images**

Kubernetes (Docker) images are the key building blocks of Containerized Infrastructure. As of now, we are only supporting Kubernetes to support Docker images. Each container in a pod has its Docker image running inside it.

When we are configuring a pod, the image property in the configuration file has the same syntax as the Docker command does. The configuration file has a field to define the image name, which we are planning to pull from the registry.

Following is the common configuration structure which will pull image from Docker registry and deploy in to Kubernetes container.

```
apiVersion: v1
kind: pod
metadata:
   name: Tesing_for_Image_pull -----------> 1
   spec:
      containers:
         - name: neo4j-server ------------------------> 2
         image: <Name of the Docker image>----------> 3
         imagePullPolicy: Always ------------->4
         command: ["echo", "SUCCESS"] ------------------->
```

In the above code, we have defined −

  1. **name: Tesing_for_Image_pull −** This name is given to identify and check what is the name of the container that would get created after pulling the images from Docker registry.
  2. **name: neo4j-server −** This is the name given to the container that we are trying to create. Like we have given neo4j-server.
  3. **image: Name of the Docker image −** This is the name of the image which we are trying to pull from the Docker or internal registry of images. We need to define a complete registry path along with the image name that we are trying to pull.
  4. **imagePullPolicy − Always -** This image pull policy defines that whenever we run this file to create the container, it will pull the same name again.
  5. command: [“echo”, “SUCCESS”] − With this, when we create the container and if everything goes fine, it will display a message when we will access the container.

In order to pull the image and create a container, we will run the following command.

```
$ kubectl create –f Tesing_for_Image_pull
```

Once we fetch the log, we will get the output as successful.

```
$ kubectl log Tesing_for_Image_pull
```

