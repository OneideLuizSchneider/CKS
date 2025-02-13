#### Network Policy - Namespaces

- Allow only ingress traffic from the namespace `namespace-example2` to the `namespace-example1`

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-specific-ingress
  namespace: namespace-example1
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:  
    - namespaceSelector:
        matchExpressions:
        - key: namespace
          operator: In
          values: ["namespace-example2"]
```

- Deny egress traffic from `namespace-exmaple` to external sites
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-external-egress
  namespace: namespace-exmaple
spec:
  podSelector: {}
  policyTypes:
  - Egress
```
or
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-external-egress
  namespace: namespace-exmaple
spec:
  podSelector: {}  # Selects all pods in namespace-exmaple
  policyTypes:
  - Egress
  egress:
  # Allow egress to all pods in all namespaces
  - to:
    - namespaceSelector: {}  # All namespaces
      podSelector: {}        # All pods
```
