#### Trivy

- <https://github.com/aquasecurity/trivy>

- Install
  ```
  https://trivy.dev/latest/getting-started/installation/

  curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin v0.59.1

  trivy version
  ```

- Scan
  - `trivy image nginx:latest`
  - `trivy image --severity HIGH,CRITICAL nginx:latest`
  - `trivy image --format json --output result.json alpine:3.15`
  - Scan a container image from a tar archive
    - `trivy image --input ruby-3.1.tar`