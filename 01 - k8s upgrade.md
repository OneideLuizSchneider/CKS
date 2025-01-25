#### Upgrade k8s Cluster


To Find the latest patch release for Kubernetes 1.31(or 1.32 or .....) using the OS package manager:
```
sudo apt update
sudo apt-cache madison kubeadm

Results:
kubeadm | 1.31.5-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
kubeadm | 1.31.4-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
kubeadm | 1.31.3-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
kubeadm | 1.31.2-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
kubeadm | 1.31.1-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
kubeadm | 1.31.0-1.1 | https://pkgs.k8s.io/core:/stable:/v1.31/deb  Packages
```

- Start with the ControlPlane Nodes:
  - Drain Node:
    `k drain controlplane --ignore-daemonsets`
  - Change packege repository version:
    - List first:
      - `pager /etc/apt/sources.list.d/kubernetes.list`
    - `nano /etc/apt/sources.list.d/kubernetes.list`
      - `deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /`
    - Ob.: if you only wanna update it, just change the version, ex. `v1.31` on the link above.

    - Run again:
      ```
      sudo apt update
      sudo apt-cache madison kubeadm
      ```
  
    - Copy the latest version
  
    - ```
      # replace x in 1.31.x-* with the latest patch version
      sudo apt-mark unhold kubeadm && \
      sudo apt-get update && sudo apt-get install -y kubeadm='1.31.x-*' && \
      sudo apt-mark hold kubeadm
      ```
    - Check the version
      - `kubeadm version`
    - Verify the upgrade plan:
      - `sudo kubeadm upgrade plan`
    - If it is all good, just run:
      - `kubeadm upgrade apply v1.31.x`
     
     
    - Upgrading Kubelet and Kubectl:
      ```
      sudo apt-mark unhold kubelet kubectl && \
      sudo apt-get update && sudo apt-get install -y kubelet='1.31.0-1.1' kubectl='1.31.0-1.1' && \
      sudo apt-mark hold kubelet kubectl
      ```
    - Restart Kubelet:
      ```
      sudo systemctl daemon-reload
      sudo systemctl restart kubelet
      ```
    - Confirm that the version is upgraded:
      - `k get nodes`
    - Now uncordo the Node:
      - `kubectl uncordon controlplane`

- Worker Nodes:
  - `ssh root@node01`
  - Upgrade kubeadm
    ```
    sudo apt-mark unhold kubeadm && \
    sudo apt-get update && sudo apt-get install -y kubeadm='1.31.0-1.1' && \
    sudo apt-mark hold kubeadm
    ```
  - Upgrade kubeadm:
    `sudo kubeadm upgrade node`
  - Drain the WorkerNode:
    `kubectl drain <node-to-drain> --ignore-daemonsets`
  - Upgrading Kubelet and Kubectl:
    ```
    sudo apt-mark unhold kubelet kubectl && \
    sudo apt-get update && sudo apt-get install -y kubelet='1.31.0-1.1' kubectl='1.31.0-1.1' && \
    sudo apt-mark hold kubelet kubectl
    ```
  - Restart Kubelet:
    ```
    sudo systemctl daemon-reload
    sudo systemctl restart kubelet
    ```
  - Confirm that the version is upgraded:
    `k get nodes`
  - Now uncordo the Node:
    `kubectl uncordon node01`

Docs:
- <https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/>