#### Container Security

- Runtime Class
  - <https://kubernetes.io/docs/concepts/containers/runtime-class/>

- gVisor - <https://gvisor.dev/>
- Kata - <https://katacontainers.io/>

- RuntimeClass example:
```
# RuntimeClass is defined in the node.k8s.io API group
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
  # The name the RuntimeClass will be referenced by.
  # RuntimeClass is a non-namespaced resource.
  name: myclass 
# The name of the corresponding CRI configuration
handler: runsc 
```

- Pod:
```
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  runtimeClassName: myclass
  # ...
```


More docs.:
- <https://github.com/opencontainers/runc>
- <https://opencontainers.org/>