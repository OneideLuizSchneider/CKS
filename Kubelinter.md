#### Kubelinter

- Repo: <https://github.com/stackrox/kube-linter>
- Install
  ```
  curl -LO https://github.com/stackrox/kube-linter/releases/latest/download/kube-linter-linux.tar.gz
  tar -xvf kube-linter-linux.tar.gz
  mv kube-linter /usr/local/bin/
  ```

- To test it:
  - `kube-linter lint /path/nginx.yml`