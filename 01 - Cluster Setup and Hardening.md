### Cluster Setup and Hardening

- CIS Benchmark
  - CIS -> Center for Internet Secutiry
    - <https://www.cisecurity.org/>

- Kube-bench
  - Install:
    - <https://github.com/aquasecurity/kube-bench/blob/main/docs/installation.md#download-and-install-binaries>
    - Example:
        ```
        curl -L https://github.com/aquasecurity/kube-bench/releases/download/v0.6.2/kube-bench_0.6.2_linux_amd64.tar.gz -o kube-bench_0.6.2_linux_amd64.tar.gz

        tar -xvf kube-bench_0.6.2_linux_amd64.tar.gz

        # to run it
        ./kube-bench --config-dir `pwd`/cfg --config `pwd`/cfg/config.yaml 
        ```

- Auth
  - Types of Auth:
    -  Static Password Files
       -  CSV file with Users, Pass and Groups
    -  Static Token Files
       -  CSV file with Tokens
    -  Cerficiates
       -  <https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/>
    -  Indentity Services
    - With Bootstrap token Secrets:
      - <https://kubernetes.io/docs/concepts/configuration/secret/#bootstrap-token-secrets>
      - TOKEN format(decoded): `<token-id>.<token-secret>`
        - Example: `./help/bootstrap-token-secret-base64.yaml`
      - curl -X GET $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure

- Generate token to bootstrap a new node:
  - Doc.: <https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-token/>
  - Example: `kubeadm token create 123465.qwe345tgiopas906 --dry-run --print-join-command --ttl 2h`
  - Ensure that kubeadm, kubelet, and kubectl are installed

- Auth Mechanisms:
  - Node 
    - Node Authorization
  - ABAC 
    - Attribute-Based Authorization
  - RBAC 
    - Role-Based Authorization
  - Webhook