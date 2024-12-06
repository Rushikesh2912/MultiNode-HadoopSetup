# Hadoop Cluster Setup

This guide helps you set up a Hadoop cluster with 6 machines: 1 Namenode (NN), 1 JobTracker (JT), and 4 DataNodes (DN1, DN2, DN3).

## Prerequisites
- 6 EC2/VM machines with Ubuntu.
- SSH access between all machines using the same private key.

## Steps

### 1. **Launch Machines and Configure DNS**
- Launch 6 machines (NN, SNN, JT, DN1, DN2, DN3).
- Update `/etc/hosts` on each machine with their private IPs.

### 2. **Passwordless SSH Login**
- Copy the SSH key to each machine and set proper permissions.
- Add the key to the SSH agent for passwordless login:
  ```bash
  eval `ssh-agent`
  ssh-add /home/ubuntu/.ssh/key.pem
## Install DSH (Distributed Shell)
sudo apt install dsh

### 3. Install DSH (Distributed Shell)
sudo apt install dsh

### 4. Install Java and Hadoop
dsh -a sudo apt install openjdk-8-jre -y
dsh -a wget https://archive.apache.org/dist/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
dsh -a sudo mv hadoop-1.2.1 /usr/local/hadoop

### 5. Configure Environment Variables
export HADOOP_PREFIX=/usr/local/hadoop/
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

### 6. Update Hadoop Configuration
Update Hadoop config files (core-site.xml, mapred-site.xml, slaves, masters) with the correct hostnames and paths.

### 7. Format Namenode and Start Services
hadoop namenode -format

## Start the DFS and MapReduce services:
start-dfs.sh
start-mapred.sh

### 8. Verify the Cluster
Check the status of Java processes with dsh -a jps.


# Notes
Replace IPs and hostnames with your actual values.
Ensure all machines are connected and accessible via private IPs.
