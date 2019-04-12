# centos7
centos7 Initialization script (Google Cloud VM instance)

# Steps
* Disable firewalld, download and enable iptables
```bash

```
* Puttygen generate ssh key, and add public key to GCP Compute Engine Metadata, in order to ssh from putty
* Disable selinux
```bash
sudo sed -i 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/selinux/config
```
* Change ssh port from 22 to port 6666
```bash
sudo sed -i 's/^#Port 22/Port 6666/g' /etc/ssh/sshd_config
```
* Download some common tools


* Restart server
```bash
sudo shutdown -r now
```

