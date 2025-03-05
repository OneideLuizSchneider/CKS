#### Cilium examples

Deny traffic from frontend pod to the database pod:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
  name: "deny-ingress"
  namespace: "default"
spec:
  endpointSelector:
    matchLabels:
      role: mypod-database
  ingressDeny:
    - fromEndpoints:
        - matchLabels:
            role: mypod-front
```

Deny egress from the front pod to the Database pod:
```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
  name: "deny-egress"
  namespace: "default"
spec:
  endpointSelector:
    matchLabels:
      role: front
  egressDeny:
    - toEndpoints:
        - matchLabels:
            role: database
```