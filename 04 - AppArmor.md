## AppArmor

- Doc:
  - <https://kubernetes.io/docs/tutorials/security/apparmor/>

- Status:
  - `aa-status`
  - `systemctl status apparmor`
    - ```
      ● apparmor.service - Load AppArmor profiles
          Loaded: loaded (/lib/systemd/system/apparmor.service; enabled; vendor pres>
          Active: active (exited) since Sat 2025-02-01 17:38:41 UTC; 54s ago
            Docs: man:apparmor(7)
               https://gitlab.com/apparmor/apparmor/wikis/home/
        Process: 582 ExecStart=/lib/apparmor/apparmor.systemd reload (code=exited, >
       Main PID: 582 (code=exited, status=0/SUCCESS)
          CPU: 115ms

      Feb 01 17:38:40 oneide systemd[1]: Starting Load AppArmor profiles...
      Feb 01 17:38:40 oneide apparmor.systemd[582]: Restarting AppArmor
      Feb 01 17:38:40 oneide apparmor.systemd[582]: Reloading AppArmor profiles
      Feb 01 17:38:41 oneide apparmor.systemd[609]: Skipping profile in /etc/apparmor>
      Feb 01 17:38:41 oneide systemd[1]: Finished Load AppArmor profiles.
      ```
    - ` cat /sys/module/apparmor/parameters/enabled`
      - `Y`

- `apt-get install -y apparmor-utils`

- Profiles:
  - `cat /sys/kernel/security/apparmor/profiles`

#### Create an `AppArmor` profile

- Default Path:
  - `/etc/apparmor.d/...`

- Deny Write Example:
  - Create a file with the content below and the name `apparmor-deny-write`:
    ```
    profile apparmor-deny-write flags=(attach_disconnected) {
      file,
      # Deny all file writes.
      deny /** w,
    }
    ```
  - Apply it:
    - `sudo apparmor_parser -q apparmor-deny-write`

- Create a pod:
  - `kubectl apply -f ./help/pod-sleeper.yml`
  - `kubectl exec ubuntu-sleeper -- cat /proc/1/attr/current`
    - Response: `apparmor-deny-write (enforce)`
  - `kubectl exec -ti ubuntu-sleeper -- touch /tmp/anyfile`
    ```
    touch: cannot touch '/tmp/test': Permission denied
    command terminated with exit code 1
    ```
