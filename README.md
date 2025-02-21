# 🚀Local Setup for Hadoop, Spark, and MinIO Storage for Spark Warehousing Housekeeping

## 📌 Prerequisites

### 🍺 Homebrew Installation

1. Set up Homebrew on macOS:

2. Install Homebrew via the Mac Self Service Portal.

3. Verify the installation in the terminal:
```
command -v brew
```
- Expected Output:
```
/opt/homebrew/bin/brew
```
4. Add Homebrew to your system path by updating both ~/.zshrc and ~/.bashrc:
```
echo 'export PATH=/opt/homebrew/bin:$PATH' | tee -a ~/.zshrc ~/.bashrc
```
5. Apply the changes:
```
source ~/.zshrc && source ~/.bashrc
```

### ☕ Java Installation

1. Install Azul Java JDK 8.70.0.23:

2. Download Azul Java JDK Version 8.70.0.23 via the Mac Self Service Portal.

3. Update both ~/.zshrc and ~/.bashrc with the following command:
```
echo 'export JAVA_HOME=$(/usr/libexec/java_home)' | tee -a ~/.zshrc ~/.bashrc
echo 'export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home' | tee -a ~/.zshrc ~/.bashrc
```
4. Apply the changes:
```
source ~/.zshrc && source ~/.bashrc
```
5. Verify Java installation:
```
java -version
```
- Expected Output:
```
openjdk version "1.8.0_xxx"
```

### 🚀 Maven Installation

1. Install Maven using Homebrew:
```
brew install maven
```
2. Add Maven environment variables to both ~/.zshrc and ~/.bashrc:
```
echo 'export M2_HOME=/Users/akhan396/apache-maven-3.8.6' | tee -a ~/.zshrc ~/.bashrc
echo 'export PATH=$PATH:$M2_HOME/bin' | tee -a ~/.zshrc ~/.bashrc
```
3. Apply the changes:
```
source ~/.zshrc && source ~/.bashrc
```
4. Verify the installation:
```
mvn -version
```
- Expected Output:
```
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /opt/homebrew/Cellar/maven/3.9.9/libexec
Java version: 1.8.0_372, vendor: Azul Systems, Inc., runtime: /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/jre
Default locale: en_IN, platform encoding: UTF-8
OS name: "mac os x", version: "14.x", arch: "aarch64", family: "mac"
```

### 🛠 Git Installation

1. Install Git using Homebrew:
```
brew install git
```
2. Verify the installation:
```
git --version
```

### 🐍 Scala Installation

1. Install Scala (version 2.13) using Homebrew:
```
brew install scala@2.13
```
2. Add Scala environment variable to both ~/.zshrc and ~/.bashrc:
```
echo 'export SCALA_HOME=/usr/local/opt/scala@2.13' | tee -a ~/.zshrc ~/.bashrc
```
3. Apply the changes:
```
source ~/.zshrc && source ~/.bashrc
```
4. Verify the installation:
```
scala -version
```

### 🌐 Proxy Configuration

1. For network access, set up proxy variables in both ~/.zshrc and ~/.bashrc:
```
export HTTP_PROXY="http://proxy.aexp.com:8080/"
export HTTPS_PROXY="https://proxy.aexp.com:8080/"
export NO_PROXY="localhost,127.0.0.1,.aexp.com"
```
2. Apply the changes:
```
source ~/.zshrc && source ~/.bashrc
```

## 🔑 IIQ Request & SSH Setup

### 📝 Raise IIQ Request

1. Raise an IIQ Request for your Mac with the name PRC-AXP-BA-E3-AppUser-macOS-TEMP-ADMIN from 👉 [IIQ Request Portal](https://iiq.aexp.com/iam/newUIPOC.jsf).

2. Wait for approval to gain IIQ Access.

3. Once approved, go to Self Service and enable Make Me Admin - Engineer.

### 🔒 SSH Installation

1. Enable Make Me Admin in Self Service.

2. Set up proxy variables in your terminal:
```
export HTTP_PROXY="http://proxy.aexp.com:8080/"
export HTTPS_PROXY="https://proxy.aexp.com:8080/"
```
3. Install OpenSSH using Homebrew:
```
brew install openssh
```
4. Verify SSH installation:
```
ssh -V
```
- Expected Output:
```
OpenSSH_9.9p1, OpenSSL 3.4.0 22 Oct 2024
```

### 🔑 Setup SSH Key

1. Generate an SSH key:
```
ssh-keygen -t rsa -P ""
```
2. Press Enter to accept the default location and set a passphrase (optional but recommended).

3. Add your SSH key to authorized_keys:
```
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

### 🔒 SSH enable

1. On terminal:
```
sudo systemsetup -setremotelogin on
```
- If the user is not in the sudoers file, click on Make Me Admin in Self Service.
  
2. Verify remote login status:
```
sudo systemsetup -getremotelogin
```
- Expected output:
```
Remote Login: On
```
3. Verify SSH access to localhost (Admin access required):
```
ssh localhost
```
### 🔍 Troubleshooting SSH

1. Check if SSH is listening:
```
sudo lsof -i :22
```
2. If no output appears, SSH may not be listening. Restart SSH:
```
sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
```
3. Restart SSH manually:
```
sudo launchctl stop com.openssh.sshd
sudo launchctl start com.openssh.sshd
```
4. If SSH is still not working, install OpenSSL and retry:
```
brew install openssl
```
- Ensure SSH version is brew by running :
```
which ssh
```

## Hadoop Installation Setup 

### 🛠️ Install Hadoop 
```bash
brew install hadoop
```

### 📝 Update Configuration Files 
Add these lines to your `.zshrc` and `.bashrc` file:
```bash
export HADOOP_HOME=/<enter your path>/ntr-recon-e0/hadoop
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/<enter your path>/ntr-recon-e0/hadoop/share/hadoop/tools/lib/*
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
```

### Clone Repository 🌍
```bash
git clone https://github.aexp.com/banan7/ntr-recon-e0
```

### Configure Hadoop ⚙️
Open the repo and edit the `ntr-e0/hadoop/etc/hadoop/hdfs-site.xml` file. Ensure the following properties match your `ntr-e0` directory:
```xml
<property>
    <name>dfs.datanode.data.dir</name>
    <value>file:///<enter your path of ntr-recon-e0>/ntr-recon-e0/vol/hadoop_data/datanode</value>
</property>
<property>
    <name>dfs.namenode.name.dir</name>
    <value>file:///<enter your path of ntr-recon-e0>/ntr-e0/vol/hadoop_data/namenode</value>
</property>
```
Ensure `<value>(path)</value>` matches correctly.

## Start HDFS and YARN 🚀

### Format HDFS Before First Use 📌
```bash
hdfs namenode -format -force
```

### Start Hadoop Services ✅
```bash
start-dfs.sh && start-yarn.sh
```

### Verify Running Services 🧐
```bash
jps
```
**Expected Output:**
```
22343 ResourceManager
22135 SecondaryNameNode
21879 NameNode
21992 DataNode
15499 Main
```

**If `namenode` or `datanode` are missing:**
```bash
hdfs namenode -format  # If needed
hdfs datanode -format  # If needed
```

**If NameNode is stuck in SafeMode:**
```bash
hdfs dfsadmin -safemode leave
```
Then, go to Self-Service and select **Make Me Admin**.

## Verify Hadoop Cluster ✅
- **HDFS NameNode UI:** [http://localhost:9870](http://localhost:9870)
- **YARN ResourceManager UI:** [http://localhost:8088/cluster](http://localhost:8088/cluster)

## Test HDFS Functionality 📂
```bash
# Create a directory
hdfs dfs -mkdir /ntr

# Put a local file into HDFS
hdfs dfs -put ./nbachamps.txt /

# List files in HDFS
hdfs dfs -ls /
```

## Stop Hadoop Services 🛑
```bash
stop-dfs.sh && stop-yarn.sh
```

