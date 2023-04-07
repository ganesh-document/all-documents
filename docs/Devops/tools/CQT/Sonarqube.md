## How to Install SonarQube on Ubuntu 20.04 LTS

* Prerequisites:
	* Ubuntu 20.04 LTS with minimum 2GB RAM and 1 CPU.
	* PostgreSQL Version 9.3 or higher
	* SSH access with sudo privileges
	* Firewall Port: 9000

* Hardware requirements:
	1. A small-scale (individual or small team) instance of the SonarQube server requires at least 2GB of RAM to run efficiently and 1GB of free RAM for the OS. If you are installing an instance for a large 	    team or an enterprise, please consider the additional recommendations below.
	2. The amount of disk space you need will depend on how much code you analyze with SonarQube.
	3. SonarQube must be installed on hard drives that have excellent read & write performance. Most importantly, the "data" folder houses the Elasticsearch indices on which a huge amount of I/O will be               done when the server is up and running. Read and write hard drive performance will therefore have a big impact on the overall SonarQube server performance.

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

* Enterprise hardware recommendations:
For large teams or enterprise-scale installations of SonarQube, additional hardware is required. At the enterprise level, monitoring your SonarQube instance is essential and should guide further hardware upgrades as your instance grows. A starting configuration should include at least:
	* 8 cores, to allow the main SonarQube platform to run with multiple compute engine workers
	* 16GB of RAM For additional requirements and recommendations relating to database and Elasticsearch.

Supported platforms:
	1. Java: The SonarQube server requires Java version 17 and the SonarQube scanners require Java version 11 or 17.
	2. Database: PostgreSQL version = 11,12,13,14,15
	3. xxxxxx: xxxxx 


To Increase the vm.max_map_count kernal ,file discriptor and ulimit permanently . Open the below config file and Insert the below value as shown below,

```
sudo vi /etc/security/limits.conf
```
```
sonarqube   -   nofile   65536
sonarqube   -   nproc    4096
```

OR If you are using systemd to manage the sonarqube services then add below value in sonarqube unit file under [service] section.

```
[Service]
...
LimitNOFILE=65536
LimitNPROC=4096
...
```

Before installing, Lets update and upgrade System Packages

```
sudo apt-get update
sudo apt-get upgrade
```

Install wget and unzip package

```
sudo apt-get install wget unzip -y
```


## Step #1: Install OpenJDK
Install OpenJDK and JRE 11 using following command,

```
sudo apt-get install openjdk-11-jdk -y
sudo apt-get install openjdk-11-jre -y
```
