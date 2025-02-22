#### K8s Audit

- <https://kubernetes.io/docs/tasks/debug/debug-cluster/audit/>

```
apiVersion: audit.k8s.io/v1
kind: Policy
omitStages:
  - "RequestReceived"
rules:
  - namespaces: ["default"]
    level: RequestResponse
    resources:
    - group: ""
      resources: ["pods"]
      resourceNames: ["my-nginx-pod"]

  - level: Metadata
    resources:
    - group: ""
      resources: ["secrets"]

```

Enable it on the `kube-apiserver`:
```
  - --audit-policy-file=/etc/kubernetes/audit-policy.yaml
  - --audit-log-path=/var/log/kubernetes/audit/audit.log
```

- Add this in the kubeapiserver manifest:
  - Add the `Volumes`:
  ```
    - name: audit
      hostPath:
        path: /etc/kubernetes/audit-policy.yaml
        type: File

    - name: audit-log
      hostPath:
        path: /var/log/kubernetes/audit/audit.log
        type: FileOrCreate
  ```
  - and `Volume Mounts`:
  ```
    - mountPath: /etc/kubernetes/audit-policy.yaml
      name: audit
      readOnly: true
    - mountPath: /var/log/kubernetes/audit/audit.log
      name: audit-log
      readOnly: false
  ```