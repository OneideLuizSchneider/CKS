#### SSH Hardening

- Generate SSH key:
  - `ssh-keygen –t rsa`
    - `Public Key: /home/user/.ssh/id_rsa.pub`
    - `Private Key: /home/user/.ssh/id_rsa`
  - Disable Root login:
    - Edit the file `vi /etc/ssh/sshd_config` and change it to:
      ```
      PermitRootLogin no
      PasswordAuthentication no
      ```
    - Restart sshd:
      -  `systemctl restart sshd`

- Creating an user and the conf to ssh it:
  - `ssh-copy-id -i ~/.ssh/id_rsa.pub roger@myhost`
- to edit the permissions for that user:
  - `vi /etc/sudoers`
  - add `roger    ALL=(ALL:ALL) ALL`
  - with pass:
    - `roger  ALL=(ALL) NOPASSWD:ALL`
  - to add the user to a group:
    - `usermod roger -G admin`
