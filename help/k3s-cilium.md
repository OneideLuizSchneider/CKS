#### k3s + Cilium

Install:
```
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC='--flannel-backend=none --disable-network-policy --disable=traefik' sh

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml

curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

helm repo add cilium https://helm.cilium.io/
helm upgrade --install cilium cilium/cilium --version 1.16.6 \
  --set operator.replicas=1 \
  --namespace kube-system
```

Uninstall:
`/usr/local/bin/k3s-uninstall.sh`