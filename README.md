# centos7
centos7 Initialization script (Google Cloud VM instance)<br>
for system administrators

# Steps
* Disable firewalld, download and enable iptables
```bash
sudo systemctl stop firewalld.service
sudo systemctl disable firewalld.service 
sudo yum install iptables-services
sudo sed -i '/--dport 22/a-A INPUT -p tcp -m state --state NEW -m tcp --dport 6666 -j ACCEPT' /etc/sysconfig/iptables
sudo systemctl start iptables.service
sudo systemctl enable iptables.service
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
```bash
sudo yum -y install wget
sudo yum -y install telnet telnet-server xinetd
sudo systemctl enable telnet.socket
sudo systemctl start telnet.socket
sudo systemctl enable xinetd
sudo systemctl start xinetd
sudo yum -y install net-tools
sudo yum -y install traceroute
sudo yum -y install lsof
sudo yum -y install sysstat
sudo yum -y install nc 
sudo yum -y install tcpdump
sudo yum -y install tree
sudo yum -y install bind-utils
sudo yum -y install nmap
sudo yum -y install git
```
* Install Docker and Docker-compose
```bash
#Docker
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo yum -y install docker-ce
sudo systemctl enable docker.service
sudo systemctl start docker.service
#Docker-compose
sudo yum -y install epel-release
sudo yum -y install python-pip
sudo pip install docker-compose
sudo yum upgrade python*
```
* Restart server
```bash
sudo shutdown -r now
```

