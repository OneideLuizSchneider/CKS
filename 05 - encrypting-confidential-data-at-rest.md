#### Encrypting Confidential Data at Rest


- Docs: 
  - <https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/>

- Example File:
  - `./help/EncryptionConfiguration.yml`
- Generate a key:
  - `head -c 32 /dev/urandom | base64`
    - Change it on the field `secret`
- Change the APIserver and add `--encryption-provider-config=/etc/kubernetes/enc/enc.yaml`:

```
...
spec:
  containers:
  - command:
    - kube-apiserver
    ...
    - --encryption-provider-config=/etc/kubernetes/enc/enc.yaml  # add this line
    ...
    volumeMounts:
    ...
    - name: enc                           # add this line
      mountPath: /etc/kubernetes/enc      # add this line
      readOnly: true                      # add this line
    ...
  volumes:
  ...
  - name: enc                             # add this line
    hostPath:                             # add this line
      path: /etc/kubernetes/enc           # add this line
      type: DirectoryOrCreate             # add this line
...      
```

- Look into a Secret with `ETCDCTL`:
  - ```
    ETCDCTL_API=3 etcdctl \
      --cacert=/etc/kubernetes/pki/etcd/ca.crt   \
      --cert=/etc/kubernetes/pki/etcd/server.crt \
      --key=/etc/kubernetes/pki/etcd/server.key  \
      get /registry/secrets/default/mysecret | hexdump -C
    ```