## How to Install SonarQube on Ubuntu 20.04 LTS

- Prerequisites:
	* Ubuntu 20.04 LTS with minimum 2GB RAM and 1 CPU.
	* PostgreSQL Version 9.3 or higher
	* SSH access with sudo privileges
	* Firewall Port: 9000

sudo sysctl -w vm.max_map_count=262144
sudo sysctl -w fs.file-max=65536
ulimit -n 65536
ulimit -u 4096

To Increase the vm.max_map_count kernal ,file discriptor and ulimit permanently . Open the below config file and Insert the below value as shown below,

sudo vi /etc/security/limits.conf
sonarqube - nofile 65536 
sonarqube - nproc 4096


 

