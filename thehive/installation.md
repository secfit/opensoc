
<div align="center">
  <h3 align="center">The Hive</h3>
</div>


## Install Java Virtual Machine
  ```sh
    yum install -y java-1.8.0-openjdk-headless.x86_64
    echo JAVA_HOME="/usr/lib/jvm/jre-1.8.0" >> /etc/environment
    export JAVA_HOME="/usr/lib/jvm/jre-1.8.0"
  ```
 
 ## Install Cassandra
 #### Add to /etc/yum.repos.d/cassandra.repo
   ```sh
    [cassandra]
    name=Apache Cassandra
    baseurl=https://downloads.apache.org/cassandra/redhat/40x/ 
    gpgcheck=1
    repo_gpgcheck=1
    gpgkey=https://downloads.apache.org/cassandra/KEYS
  ```
  
  ```sh
    yum install cassandra
  ```
  #### Configuration cassandra
  Start by changing the 'cluster_name' with 'thp': 
 ```sh
    cqlsh localhost 9042
    UPDATE system.local SET cluster_name = 'thp' where key='local';
  ```
  Exit and run
 ```sh
    nodetool flush
  ```
  #### Configure Cassandra by editing /etc/cassandra/cassandra.yaml file
   ```sh
    	cluster_name: 'thp'
	listen_address: 'xx.xx.xx.xx' # address for nodes
	rpc_address: 'xx.xx.xx.xx' # address for clients
	seed_provider:
		- class_name: org.apache.cassandra.locator.SimpleSeedProvider
		  parameters:
			  # Ex: "<ip1>,<ip2>,<ip3>"
			  - seeds: 'xx.xx.xx.xx' # self for the first node
	data_file_directories:
	  - '/var/lib/cassandra/data'
	commitlog_directory: '/var/lib/cassandra/commitlog'
	saved_caches_directory: '/var/lib/cassandra/saved_caches'
	hints_directory: 
	  - '/var/lib/cassandra/hints'
  ```
  
  #### Restart cassandra service
 ```sh
    service cassandra restart
  ```
  
## Install The Hive
Install The Hive chosing binary package:
#### Download last package
 ```sh
    cd /opt
    wget --no-check-certificate https://archives.strangebee.com/zip/thehive-latest.zip
    unzip thehive-latest.zip
    mv thehive-5.0.15-1 thehive
  ```
  #### Prepare the system
   ```sh
    groupadd thehive
    useradd --system -g thehive thehive
    chown -R thehive:thehive /opt/thehive
    mkdir /etc/thehive
    cp /opt/thehive/conf/application.conf /etc/thehive/
    chown -R root:thehive /etc/thehive
    chmod 640 /etc/thehive/application.conf
    cp /opt/thehive/conf/thehive.service /usr/lib/systemd/system/
    
    mkdir /opt/thp/thehive/index
    mkdir -p /opt/thp/thehive/files
    chown thehive:thehive -R /opt/thp/thehive/index
    chown -R thehive:thehive /opt/thp/thehive/files
    unzip thehive-latest.zip
    mv thehive-5.0.15-1 thehive
  ```
  NB: you can find config file on this (section)[https://github.com/secfit/opensoc/tree/main/the_hive_conf]
  
