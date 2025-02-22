#### Kubesec

- <https://kubesec.io/>
- Install:
  ```
  wget https://github.com/controlplaneio/kubesec/releases/download/v2.13.0/kubesec_linux_amd64.tar.gz
  tar -xvf  kubesec_linux_amd64.tar.gz
  mv kubesec /usr/bin/
  
  kubesec version
  ```
- Usage:
  - `kubesec scan my-manifest.yml`