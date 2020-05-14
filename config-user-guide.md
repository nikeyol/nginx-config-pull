# Config Sync User Guide

## Prerequisite
### Enable login without password
1. Create directory in local node if the .ssh doesn't exist
```Shell
sudo mkdir /root/.ssh

```
2. Create public and private key
```Shell
sudo ssh-keygen -t rsa -b 2048
sudo cat /root/.ssh/id_rsa.pub
```
3. Copy the public key into remote node
```Shell
sudo echo ‘ssh-rsa AAAAB3Nz4rFgt...vgaD root@node1' >> /root/.ssh/authorized_keys  
```
4. Config sshd in /etc/ssh/sshd_config and restart the sshd via "sudu systemctl restart sshd"
```text
PermitRootLogin without-password
```
5. Makre sure the ssh without password successfully.
```Shell
sudo ssh root@remote-node
```
6. Create config file in local node
```Shell
sudo echo 'NODES="node2.example.com node3.example.com node4.example.com"
CONFPATHS="/etc/nginx/nginx.conf /etc/nginx/conf.d"
EXCLUDE="default.conf" ' >> path_to_config/sync-config.conf
```
Note: please set the value "path_to_config/sync-config.conf" in variable "CONF" in sync-config-v1.sh. The default value is "/etc/sync-config.conf"

## Execution
Please modify the NODES, CONFPATHS and EXCLUDE parameter in sync-config.conf file before execution.

```shell
sudo ./sync-config-v1.sh
```
