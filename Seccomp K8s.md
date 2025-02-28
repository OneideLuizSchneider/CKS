### Seccomp

- Default location in k8s: `/var/lib/kubelet/seccomp/`

- <https://kubernetes.io/docs/reference/node/seccomp/>
- <https://kubernetes.io/docs/tutorials/security/seccomp/>

#### Steps:

- Copy the seccomp profile to the appropriate directory
```
cp ~/auditing.json /var/lib/kubelet/seccomp/profiles
```

- Change the seccomp profile by adding the below argument in the kubelet config file
```
Add 'seccompDefault: true' to /var/lib/kubelet/config.yaml

streamingConnectionIdleTimeout: 0s
syncFrequency: 0s
volumeStatsAggPeriod: 0s
seccompDefault: true
```

- Restart Kubelet
```
sudo systemctl restart kubelet
```

- Pod:
```

vi ~/seccomp-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx-auditing
spec:
  containers:
  - image: nginx
    name: nginx
  securityContext:
    seccompProfile:
      type: Localhost 
      localhostProfile: profiles/auditing.json # here

```

- Apply it:
```
kubectl apply -f ~/seccomp-pod.yaml
```