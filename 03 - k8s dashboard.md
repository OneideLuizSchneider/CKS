#### kubernetes dashboard

Doc: https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/

- Install:
  - `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml`
- Proxy:
  - `kubectl proxy --address=0.0.0.0 --disable-filter &`
  - open `http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login`
  - Get Token:
    - `kubectl get secrets -n kubernetes-dashboard admin-user -o go-template="{{.data.token | base64decode}}"`