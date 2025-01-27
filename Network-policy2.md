#### Network Policy 2

- this will allow only egress to two PODs Payroll(8080) and Mysql(3306) for the internal POD.
  - In addition, we'll add port 53 for DNS resolution and all Ingress traffic for testing purposes.

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
  - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - ports:
    - protocol: TCP
      port: 53
    - protocol: UDP
      port: 53
```


- Allow all Egress except to one ip address(192.168.0.1)

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-ip
  namespace: default
spec:
  podSelector:
    matchLabels:
      myapp: myapp
  policyTypes:
    - Egress

  egress:
    - to:
        - ipBlock:
            cidr: 0.0.0.0/0
            except:
            - 192.168.0.1/32
```
