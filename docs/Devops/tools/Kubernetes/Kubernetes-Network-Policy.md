## **Kubernetes - Network Policy**

Network Policy defines how the pods in the same namespace will communicate with each other and the network endpoint. It requires extensions/v1beta1/networkpolicies to be enabled in the runtime configuration in the API server. Its resources use labels to select the pods and define rules to allow traffic to a specific pod in addition to which is defined in the namespace.

First, we need to configure Namespace Isolation Policy. Basically, this kind of networking policies are required on the load balancers.

```
kind: Namespace
apiVersion: v1
metadata:
   annotations:
      net.beta.kubernetes.io/network-policy: |
      {
         "ingress": 
         {
            "isolation": "DefaultDeny"
         }
      }
```

```
$ kubectl annotate ns <namespace> "net.beta.kubernetes.io/network-policy = 
{\"ingress\": {\"isolation\": \"DefaultDeny\"}}"
```

Once the namespace is created, we need to create the Network Policy.

**Network Policy Yaml**

```
kind: NetworkPolicy
apiVersion: extensions/v1beta1
metadata:
   name: allow-frontend
   namespace: myns
spec:
   podSelector:
      matchLabels:
         role: backend
   ingress:
   - from:
      - podSelector:
         matchLabels:
            role: frontend
   ports:
      - protocol: TCP
         port: 6379
```

