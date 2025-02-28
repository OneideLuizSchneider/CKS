## Falco

- <https://falco.org/>
- <https://falco.org/docs/getting-started/>
- <https://falco.org/docs/setup/kubernetes/>
- <https://github.com/falcosecurity/falco>

- Falco Conf file:
  - `/etc/falco/falco.yaml`

- Look at logs:
  - `journalctl -fu falco`

- Service status:
  - `systemctl status falco`

#### Example

Lets say you need to you need to change the rule `shell in a container`, but the output needs to be "user id", "container id", "container image repo":

```
- Navigate to /etc/falco/falco_rules.yaml
- Find the rule titled "shell in a container"
```
Copy the rule to /etc/falco/falco_rules.local.yaml

Apply the changes:
```

- rule: Terminal shell in container
  desc: A shell was used as the entrypoint/exec point into a container with an attached terminal.
  condition: >
    spawned_process and container
    and shell_procs and proc.tty != 0
    and container_entrypoint
    and not user_expected_terminal_shell_in_container_conditions
  output: >
    %evt.time.s,%user.uid,%container.id,%container.image.repository
  priority: ALERT
  tags: [container, shell, mitre_execution]
  
  Save the /etc/falco/falco_rules.local.yaml file.
  
```
