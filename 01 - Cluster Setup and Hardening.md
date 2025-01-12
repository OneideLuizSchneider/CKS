### Cluster Setup and Hardening

- CIS Benchmark
  - CIS -> Center for Internet Secutiry
    - <https://www.cisecurity.org/>

- Kube-bench
  - Install:
    - <https://github.com/aquasecurity/kube-bench/blob/main/docs/installation.md#download-and-install-binaries>
    - Example:
        ```
        curl -L https://github.com/aquasecurity/kube-bench/releases/download/v0.6.2/kube-bench_0.6.2_linux_amd64.tar.gz -o kube-bench_0.6.2_linux_amd64.tar.gz

        tar -xvf kube-bench_0.6.2_linux_amd64.tar.gz

        # to run it
        ./kube-bench --config-dir `pwd`/cfg --config `pwd`/cfg/config.yaml 
        ```

- Auth
  - Types of Auth:
    -  Static Password Files
       -  CSV file with Users, Pass and Groups
    -  Static Token Files
       -  CSV file with Tokens
    -  Cerficiates
    -  Indentity Services