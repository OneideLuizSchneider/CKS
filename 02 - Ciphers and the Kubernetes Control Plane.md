#### Ciphers and the Kubernetes Control Plane

- All the control plane components (API server, controller manager, kubelet, scheduler) have the following two optional arguments:
  - `--tls-min-version`
    - This argument sets the minimum version of TLS that may be used during connection negotiation. Possible values: VersionTLS10, VersionTLS11, VersionTLS12, VersionTLS13, for TLS 1.0 thru TLS 1.3 respectively. The default is VersionTLS10.
  - `--tls-cipher-suites` 
    - This argument sets a comma-separated list of cipher suites that may be used during connection negotiation.

- `etcd` also has a command line argument to set cipher suites.
  - `--cipher-suites` – This argument sets a comma-separated list of cipher suites that may be used during connection negotiation.