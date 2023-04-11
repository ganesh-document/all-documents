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

## SET Default JDK

```
sudo update-alternatives --config java
```

## Check JAVA Version:

```
java -version
```

## Step #2: Install and Setup PostgreSQL 10 Database For SonarQube

Add and download the PostgreSQL Repo

```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
```

Install the PostgreSQL database Server by using following command,

```
sudo apt-get -y install postgresql postgresql-contrib
```

Start PostgreSQL Database server

```
sudo systemctl start postgresql
```

Enable it to start automatically at boot time.

```
sudo systemctl enable postgresql
```

Change the password for the default PostgreSQL user.

```
sudo passwd postgres
```

Switch to the postgres user.

```
su - postgres
```

Create a new user by typing:

```
createuser sonar
```

Switch to the PostgreSQL shell.

```
psql
```

Set a password for the newly created user for SonarQube database.

```
ALTER USER sonar WITH ENCRYPTED password 'sonar';
```

Create a new database for PostgreSQL database by running:

```
CREATE DATABASE sonarqube OWNER sonar;
```

grant all privileges to sonar user on sonarqube Database.

```
grant all privileges on DATABASE sonarqube to sonar;
```

Exit from the psql shell:

```
\q
```

Switch back to the sudo user by running the exit command.

```
exit
```


## Step #3: How to Install SonarQube on Ubuntu 20.04 LTS

Download sonaqube installer files archieve To download latest version of visit SonarQube (https://www.sonarsource.com/products/sonarqube/downloads/)

```
cd /tmp
sudo https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.1.44547.zip
```

Unzip the archeve setup to /opt directory

```
sudo unzip sonarqube-8.9.1.zip -d /opt
```

Move extracted setup to /opt/sonarqube directory

```
sudo mv /opt/sonarqube-8.9.1 /opt/sonarqube
```

## Step #4: Configure SonarQube

We can’t run Sonarqube as a root user , if you run using root user it stops automatically. We have found solution on this to create saparate group and user to run sonarqube.

## 1. Create Group and User:

Create a group as sonar

```
sudo groupadd sonar
```

Now add the user with directory access

```
sudo useradd -c "user to run SonarQube" -d /opt/sonarqube -g sonar sonar 
sudo chown sonar:sonar /opt/sonarqube -R
```

Open the SonarQube configuration file using your favorite text editor.

```
sudo nano /opt/sonarqube/conf/sonar.properties
```

Find the following lines.

```
#sonar.jdbc.username=
#sonar.jdbc.password=
```

Uncomment and Type the PostgreSQL Database username and password which we have created in above steps and add the postgres connection string.

```
vi /opt/sonarqube/conf/sonar.properties

#--------------------------------------------------------------------------------------------------

# DATABASE

#

# IMPORTANT:

# - The embedded H2 database is used by default. It is recommended for tests but not for

#   production use. Supported databases are Oracle, PostgreSQL and Microsoft SQLServer.

# - Changes to database connection URL (sonar.jdbc.url) can affect SonarSource licensed products.

# User credentials.

# Permissions to create tables, indices and triggers must be granted to JDBC user.

# The schema must be created first.

sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:postgresql://localhost:5432/sonarqube
```

## 2. Start SonarQube:

Now to start SonarQube we need to do following: Switch to sonar user

```
sudo su sonar
```

Move to the script directory

```
cd /opt/sonarqube/bin/linux-x86-64/
```

Run the script to start SonarQube

```
./sonar.sh start
```

We can also add this in service and can run as a service.

## 3. Check SonarQube Running Status:

To check if sonaqube is running enter below command,

```
./sonar.sh status
```

### 4. SonarQube Logs:

To check sonarqube logs, navigate to /opt/sonarqube/logs/sonar.log directory

```
tail /opt/sonarqube/logs/sonar.log
```

## Step #5: Configure Systemd service

First stop the SonarQube service as we started manually using above steps Navigate to the SonarQube installed path

```
cd /opt/sonarqube/bin/linux-x86-64/
```

Run the script to start SonarQube

```
./sonar.sh stop
```

Create a systemd service file for SonarQube to run as System Startup.

```
sudo vi /etc/systemd/system/sonar.service

Add the below lines,

[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop

User=sonar
Group=sonar
Restart=always

LimitNOFILE=65536
LimitNPROC=4096

[Install]
WantedBy=multi-user.target
```

Save and close the file. Now stop the sonarqube script earlier we started to run using as daemon. Start the Sonarqube daemon by running:

```
sudo systemctl start sonar
```

Enable the SonarQube service to automatically  at boot time System Startup.

```
sudo systemctl enable sonar
```

check if the sonarqube service is running,

```
sudo systemctl status sonar
```

## Step #6: Access SonarQube

To access the SonarQube using browser type server IP followed by port 9000.

```
http://server_IP:9000 OR http://localhost:9000
```

Login to SonarQube  with default administrator username and password is admin.

## Ref:
https://www.fosstechnix.com/how-to-install-sonarqube-on-ubuntu-20-04/


