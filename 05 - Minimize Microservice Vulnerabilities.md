## Minimize Microservice Vulnerabilities

- Cecurity Context
  - Doc: <https://kubernetes.io/docs/tasks/configure-pod-container/security-context/>
  - Example:
    - ```
      apiVersion: v1
      kind: Pod
      metadata:
        name: security-context-demo
      spec:
        securityContext:
          runAsUser: 1000
        volumes:
        - name: sec-ctx-vol
          emptyDir: {}
        containers:
        - name: sec-ctx-demo
          image: busybox:1.28
          command: [ "sh", "-c", "sleep 1h" ]
          volumeMounts:
          - name: sec-ctx-vol
            mountPath: /data/demo
          securityContext:
            allowPrivilegeEscalation: false
      ```

- Admission Controller
  - Doc: <https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/>
  - API Server flag:
    - Enable: `kube-apiserver --enable-admission-plugins=NamespaceLifecycle,LimitRanger ...`
    - Disable: `kube-apiserver --disable-admission-plugins=PodNodeSelector,AlwaysDeny ...`
      - To check it:
        - `ps -ef | grep kube-apiserver | grep admission-plugins`
  - Enable by default(k8s 1.32):
    - `CertificateApproval, CertificateSigning, CertificateSubjectRestriction, DefaultIngressClass, DefaultStorageClass, DefaultTolerationSeconds, LimitRanger, MutatingAdmissionWebhook, NamespaceLifecycle, PersistentVolumeClaimResize, PodSecurity, Priority, ResourceQuota, RuntimeClass, ServiceAccount, StorageObjectInUseProtection, TaintNodesByCondition, ValidatingAdmissionPolicy, ValidatingAdmissionWebhook`


- Pod Security
  - Pod Security Admission (PSA)
    - <https://kubernetes.io/docs/concepts/security/pod-security-admission/>
  - Pod Security Standards (PSS).
    - <https://kubernetes.io/docs/concepts/security/pod-security-standards/>
  
  - PSA is enable by default, to check it:
    - ```
      kubectl exec -n kube-system kube-apiserver-controlplane \
        -- kube-apiserver -h | grep enable-admission`
      ```
  - PS NS level:
    - Label: `pod-security.kubernetes.io/<MODE>: <LEVEL>`
      - Mode:
        - `enforce`
        - `audit`
        - `warn`
      - LevelL
        - `Privileged`
        - `Baseline`
        - `Restricted`

