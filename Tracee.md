##### Tracing Syscalls with `tracee`

- <https://github.com/aquasecurity/tracee>
- <https://aquasecurity.github.io/tracee/latest/>

Tracing the `ls` command:
```
docker run --name tracee --rm --privileged --pid=host \
  -v /lib/modules/:/lib/modules/:ro -v /usr/src:/usr/src:ro \
  -v /tmp/tracee:/tmp/tracee aquasec/tracee:0.4.0 --trace comm=ls
```

Tracing new containers:
```
sudo docker run --name tracee --rm --privileged --pid=host \
  -v /lib/modules/:/lib/modules/:ro -v /usr/src:/usr/src:ro \
  -v /tmp/tracee:/tmp/tracee aquasec/tracee:0.4.0 --trace container=new
```

Tracing new PID:
```
sudo docker run --name tracee --rm --privileged --pid=host \
  -v /lib/modules/:/lib/modules/:ro -v /usr/src:/usr/src:ro \
  -v /tmp/tracee:/tmp/tracee aquasec/tracee:0.4.0 --trace pid=new
```

#### k8s - Helm

```
helm repo add aqua https://aquasecurity.github.io/helm-charts/
helm repo update
helm install tracee aqua/tracee --namespace tracee --create-namespace

kubectl logs -f daemonset/tracee -n tracee
```