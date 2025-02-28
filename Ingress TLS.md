#### Ingress Secure 

- Doc:
  - <https://kubernetes.github.io/ingress-nginx/user-guide/tls/>

- Generate TLS cert:
```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout cert.key -out cert.crt -subj "/CN=world.universe.mine/O=mylocaldns.com"
```

- Create the TLS secret:
```
k create secret tls ingress-tls --cert=cert.crt --key=cert.key -n default
```

Add the TLS conf to the ingress:
```
spec:
  tls:
  - hosts:
    - mylocaldns.com
    secretName: ingress-tls
  rules:
  - host: mylocaldns.com
    http:
      paths:
      ....
```