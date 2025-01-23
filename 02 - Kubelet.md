#### kubelet

- Default path:
  - `/var/lib/kubelet`
- Config:
  - `/var/lib/kubelet/config.yaml`
- Default port:
  - `10250`
- Read-Only Port:
  - `10255`
  - `curl -sk http://localhost:10255/metrics`
  - to disable it:
    -  set the `readOnlyPort: 0` in `/var/lib/kubelet/config.yaml`