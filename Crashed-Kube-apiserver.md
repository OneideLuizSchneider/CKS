#### Crashed API Server

Restart the Kubelet:
`systemctl restart kubelet`

Look if the kubelet can start the apiserver:
`journalctl -fu kubelet | grep apiserver`

Take a look in the YAML file:
`/etc/kubernetes/manifests/kube-apiserver.yaml`