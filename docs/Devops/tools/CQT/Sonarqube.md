## How to Install SonarQube on Ubuntu 20.04 LTS

** Prerequisites:
	* Ubuntu 20.04 LTS with minimum 2GB RAM and 1 CPU.
	* PostgreSQL Version 9.3 or higher
	* SSH access with sudo privileges
	* Firewall Port: 9000

** Hardware requirements:
	* A small-scale (individual or small team) instance of the SonarQube server requires at least 2GB of RAM to run efficiently and 1GB of free RAM for the OS. If you are installing an instance for a large 	    team or an enterprise, please consider the additional recommendations below.
	* The amount of disk space you need will depend on how much code you analyze with SonarQube.
	* SonarQube must be installed on hard drives that have excellent read & write performance. Most importantly, the "data" folder houses the Elasticsearch indices on which a huge amount of I/O will be done 	    when the server is up and running. Read and write hard drive performance will therefore have a big impact on the overall SonarQube server performance.

```
sudo sysctl -w vm.max_map_count=262144
```
```
sudo sysctl -w fs.file-max=65536
```
```
ulimit -n 65536
```
```
ulimit -u 4096
```



To Increase the vm.max_map_count kernal ,file discriptor and ulimit permanently . Open the below config file and Insert the below value as shown below,

```
sudo vi /etc/security/limits.conf
```
```
sonarqube - nofile 65536
```
``` 
sonarqube - nproc 4096
```


 

