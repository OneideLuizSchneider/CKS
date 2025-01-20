#### TLS Certificates

- Private Keys Names(Usually):
  - *.key, *-key.pem
  - server.key
  - server-key.pem
  - client.key
  - client-key.pem
- Public Key Names(Usually):
  - *.cert, *.pem
  - server.crt
  - server.pem
  - client.crt
  - client.pem

#### TLS in Kubernetes

- Doc: <https://kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/>
  
- SSL Keys:
  - <https://kubernetes.io/docs/tasks/administer-cluster/certificates/>
    ```
    openssl genrsa -out ca.key 2048
    openssl req -new -key ca.key -out ca.csr -subj "/CN=KUBERNETES-CA"
    openssl x509 req -in ca.csr -signkey ca.key -out ca.crt
    openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt

    # view the certificates
    openssl req  -noout -text -in ./ca.csr
    openssl x509  -noout -text -in ./ca.crt
    ```
    
    ```
    # view k8s certs on the Master nodes
    openssl x509 -in /etc/kubernetes/pki/ca.crt -text -noout
    openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
    openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text -noout
    openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout
    openssl x509 -in /etc/kubernetes/pki/ca.crt -text -noout
    ```