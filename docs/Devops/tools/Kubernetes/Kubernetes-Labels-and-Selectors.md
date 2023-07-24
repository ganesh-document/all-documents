## **Kubernetes - Labels & Selectors**

**Labels**

Labels are key-value pairs which are attached to pods, replication controller and services. They are used as identifying attributes for objects such as pods and replication controller. They can be added to an object at creation time and can be added or modified at the run time.

**Selectors**

Labels do not provide uniqueness. In general, we can say many objects can carry the same labels. Labels selector are core grouping primitive in Kubernetes. They are used by the users to select a set of objects.

**Kubernetes API currently supports two type of selectors −**

  1. **Equality-based selectors**
  2. **Set-based selectors**

**Equality-based Selectors**

They allow filtering by key and value. Matching objects should satisfy all the specified labels.

**Set-based Selectors**

Set-based selectors allow filtering of keys according to a set of values.

```
apiVersion: v1
kind: Service
metadata:
   name: sp-neo4j-standalone
spec:
   ports:
      - port: 7474
      name: neo4j
   type: NodePort
   selector:
      app: salesplatform ---------> 1
      component: neo4j -----------> 2
```

In the above code, we are using the label selector as **app: salesplatform** and component as **component: neo4j**.

Once we run the file using the **kubectl** command, it will create a service with the name **sp-neo4j-standalone** which will communicate on port 7474. The ype is **NodePort** with the new label selector as **app: salesplatform** and **component: neo4j**.

