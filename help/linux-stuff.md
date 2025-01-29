#### Linux stuff

##### Users
```
id root
cat /etc/shadow
cat /etc/group
cat /etc/password
cat /etc/passwd

# set new pass for user
passwd roger

# delete user
userdel roger

# delete group
groupdel devgroup

# suspend an user
usermod -s /usr/sbin/nologin roger

# create user in the folder /opt/ and in the admin group with the id 2328
useradd -d /opt/roger -s /bin/bash -G admin -u 2328 roger
```

##### Services

- To list all services:
  - `systemctl list-units --type service`
- Path of services:
  - `/lib/systemd/system`

##### Restrict Kernel

- List all modules:
  - `lsmod`
- Blacklist
  - `modprobe` intelligently adds or removes a module from the Linux kernel.<https://linux.die.net/man/8/modprobe>
    - To blacklist modules:
      - `cat /etc/modprobe.d/blacklist.conf`
      - ...and add: 
      - `blacklist sctp`
      - Reboot the system

##### Ports

- Listen all ports:
  - `netstat -an | grep –w LISTEN`
- Look for ports on services:
  - `netstat -natp  | grep 9090`
  - `cat /etc/services | grep –w 53` 
