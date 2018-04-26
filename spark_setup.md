1. Run docker image in the master instance by running cli from the following markdown
https://github.com/YCCZhao/NYC_Traffic_Analysis_Using_Taxi_Data/blob/master/docker_setup.md

**Once you did the "docker run....." commands, jupyter notebook is run. 
You can open it using the instruction provided in the terminal 

2. Create worker instances. Number of instance and instance types depend on your need, im using 3 m5.xlarge worker nodes.

3. download and install anaconda in each instance. 
https://repo.continuum.io/archive/Anaconda3-5.1.0-Linux-x86_64.sh

4. do following in all instance:
```sudo apt-get update
sudo apt-get -y install openjdk-8-jdk-headless
mkdir ~/server
cd ~/server
wget http://mirror.reverse.net/pub/apache/spark/spark-2.3.0/spark-2.3.0-bin-hadoop2.7.tgz
tar xvzf spark-2.3.0-bin-hadoop2.7.tgz
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
```

5. start master node:
do the following in the master instance
```cd ~/server
./spark-2.1.0-bin-hadoop2.7/sbin/start-master.sh
```
 
6. then a spark job is started. Job status is shown in IP.address:8080.
ex: mine is ec2-13-57-247-150.us-west-1.compute.amazonaws.com:8080
Once you are in that page, copy the address start with spark://.....

7. Now start the worker nodes:
do the following in the worker instances
```cd ~/server
./spark-2.3.0-bin-hadoop2.7/sbin/start-slave.sh spark://...
``` 
