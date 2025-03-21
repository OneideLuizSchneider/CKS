# Certified Kubernetes Security Specialist (CKS) Exam Tips and beyond

Helpful tips to achieve CKS certification.

## Resources I used for the Exam Preparation

- Kubernetes [Official Documentation](https://kubernetes.io/docs/home/), for sure!
- Killer Shell [CKS Exam Simulator](https://killer.sh/cks)
- ...and the most important:
  - Repeat, Repeat and Repeat...

## Local Env. for Tests and messing around

- Minikube:
  - <https://minikube.sigs.k8s.io/docs/start/>
  - `minikube start --driver=docker --network-plugin=cni`
  - CNI: 
    - ./help/cilium.md
  - Pause and unpause k8s:
    - `minikube pause`
    - `minikube unpause`

## CKS Curriculum until ......

- Cluster Setup 10%
  - Use Network security policies to restrict cluster level access
  - Use CIS benchmark to review the security configuration of Kubernetes components (etcd, kubelet, kubedns, kubeapi)
  - Properly set up Ingress objects with security control
  - Protect node metadata and endpoints
  - Minimize use of, and access to, GUI elements
  - Verify platform binaries before deploying

- Cluster Hardening 15%
  - Restrict access to Kubernetes API
  - Use Role Based Access Controls to minimize exposure
  - Exercise caution in using service accounts e.g. disable defaults, minimize permissions on newly created ones
  - Update Kubernetes frequently

- System Hardening 15%
  - Minimize host OS footprint (reduce attack surface)
  - Minimize IAM roles
  - Minimize external access to the network
  - Appropriately use kernel hardening tools such as AppArmor, seccomp

- Minimize Microservice Vulnerabilities 20%
  - Setup appropriate OS level security domains
  - Manage Kubernetes secrets
  - Use container runtime sandboxes in multi-tenant environments (e.g. gvisor, kata containers)
  - Implement pod to pod encryption by use of mTLS

- Supply Chain Security 20%
  - Minimize base image footprint
  - Secure your supply chain: whitelist allowed registries, sign and validate images
  - Use static analysis of user workloads (e.g.Kubernetes resources, Docker files)
  - Scan images for known vulnerabilities

- Monitoring, Logging and Runtime Security 20%
  - Perform behavioral analytics of syscall process and file activities at the host and container level to detect malicious activities
  - Detect threats within physical infrastructure, apps, networks, data, users and workloads
  - Detect all phases of attack regardless where it occurs and how it spreads
  - Perform deep analytical investigation and identification of bad actors within environment
  - Ensure immutability of containers at runtime
  - Use Audit Logs to monitor access
- Doc:
  - <https://github.com/cncf/curriculum/>
