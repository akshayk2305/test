# 📌 Local Setup for Hadoop, Spark, and Local S3 MinIO Storage  

This guide provides step-by-step instructions to set up **Hadoop, Spark, and MinIO** on your local machine. Follow these steps to ensure a smooth installation.  

---

## ⚡ Prerequisites  

### 🍺 Install Homebrew  

1️⃣ Install **Homebrew** through the **Mac Self Service Portal**.  
2️⃣ Verify the installation in the terminal:  

   ```bash
   command -v brew
   ```  

   **Expected Output:**  
   ```
   /opt/homebrew/bin/brew
   ```

3️⃣ Update your shell configuration (`.zshrc` & `.bashrc`) to include Homebrew in the system path:  

   ```bash
   export PATH=/opt/homebrew/bin:$PATH
   ```  

### ☕ Install Java (Azul JDK 8)  

1️⃣ Download **Azul Java JDK Version 8.70.0.23** via the **Self Service Portal**.  
2️⃣ Open your terminal and edit your shell configuration:  

   ```bash
   nano ~/.zshrc  # or nano ~/.bashrc
   ```  

3️⃣ Add the following lines at the end of the file:  

   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home)
   export JAVA_HOME=/Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
   ```  

4️⃣ Save the file (`CTRL + X`, then `Y`, then `Enter`).  
5️⃣ Apply the changes:  

   ```bash
   source ~/.zshrc  # or source ~/.bashrc
   ```  

6️⃣ Verify the installation:  

   ```bash
   java -version
   ```  

   **Expected Output:**  
   ```
   openjdk version "1.8.0_xxx"
   ```  

### ⚡ Maven Installation  

1️⃣ Install **Maven** using Homebrew:  
   ```bash
   brew install maven
   ```  

2️⃣ Update your shell configuration (`.zshrc` & `.bashrc`):  
   ```bash
   export M2_HOME=/Users/akhan396/apache-maven-3.8.6
   export PATH=$PATH:$M2_HOME/bin
   ```  

3️⃣ Verify the installation:  
   ```bash
   mvn -version
   ```  

   **Expected Output:**  
   ```
   Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
   Maven home: /opt/homebrew/Cellar/maven/3.9.9/libexec
   Java version: 1.8.0_372, vendor: Azul Systems, Inc., runtime: /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home/jre
   Default locale: en_IN, platform encoding: UTF-8
   OS name: "mac os x", version: "14.x", arch: "aarch64", family: "mac"
   ```  

### 🔹 Git Installation  

1️⃣ Install **Git** using Homebrew:  
   ```bash
   brew install git
   ```  

2️⃣ Verify the installation:  
   ```bash
   git --version
   ```  

### 🔥 Scala Installation  

1️⃣ Install **Scala 2.13** using Homebrew:  
   ```bash
   brew install scala@2.13
   ```  

2️⃣ Verify the installation:  
   ```bash
   scala -version
   ```  

3️⃣ Update your shell configuration (`.zshrc` & `.bashrc`):  
   ```bash
   export SCALA_HOME=/usr/local/opt/scala@2.13
   ```  

### 🌐 Proxy Configuration  

1️⃣ Update your shell configuration (`.zshrc` & `.bashrc`) with the following proxy settings:  
   ```bash
   export HTTP_PROXY="http://proxy.aexp.com:8080/"
   export HTTPS_PROXY="https://proxy.aexp.com:8080/"
   export NO_PROXY="localhost,127.0.0.1,.aexp.com"
   ```  

### 🛠️ IIQ Access Request  

1️⃣ Raise an **IIQ Request** for your Mac with the name:  
   **PRC-AXP-BA-E3-AppUser-macOS-TEMP-ADMIN**  
   ➡️ [IIQ Request Portal](https://iiq.aexp.com/iam/newUIPOC.jsf)  

2️⃣ Once approved, you will receive **IIQ Access**.  
3️⃣ Navigate to **Self Service** and enable:  
   **Make Me Admin - Engineer**  

---

## 🔐 SSH Installation  

1️⃣ Enable **Make Me Admin** on Self Service.  

2️⃣ Set up proxy environment variables in `.zshrc` & `.bashrc`:  
   ```bash
   export HTTP_PROXY="http://proxy.aexp.com:8080/"
   export HTTPS_PROXY="https://proxy.aexp.com:8080/"
   ```  

3️⃣ Install **OpenSSH** using Homebrew:  
   ```bash
   brew install openssh
   ```  

4️⃣ Verify installation:  
   ```bash
   ssh -V
   ```  
   **Expected Output:**  
   ```
   OpenSSH_9.9p1, OpenSSL 3.4.0 22 Oct 2024
   ```  

5️⃣ Generate SSH Key:  
   ```bash
   ssh-keygen -t rsa -P ""
   ```  
   ➡️ Press **Enter** for the default location.  
   ➡️ Set a **passphrase** (optional but recommended).  

6️⃣ Add the key to `authorized_keys`:  
   ```bash
   cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
   ```  

---

## 🚀 Enabling SSH  

1️⃣ Enable **Remote Login**:  
   ```bash
   sudo systemsetup -setremotelogin on
   ```  

   If you encounter a *sudoers file error*, click **Make Me Admin** in Self Service.  

2️⃣ Verify Remote Login status:  
   ```bash
   sudo systemsetup -getremotelogin
   ```  
   **Expected Output:**  
   ```
   Remote Login: On
   ```  

3️⃣ Test SSH connection to localhost:  
   ```bash
   ssh localhost
   ```  
   ➡️ **Admin access is required.**  

---

## 🛠️ Troubleshooting SSH Issues  

1️⃣ Check if SSH is listening on port 22:  
   ```bash
   sudo lsof -i :22
   ```  
   If **no output**, restart SSH:  
   ```bash
   sudo launchctl unload /System/Library/LaunchDaemons/ssh.plist
   sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist
   ```  

2️⃣ Restart SSH service:  
   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```  

3️⃣ If SSH issues persist, install OpenSSL and retry:  
   ```bash
   brew install openssl
   ```  

4️⃣ Check which SSH binary is being used:  
   ```bash
   which ssh
   ```  

---

## 🚀 Hadoop Installation & Setup

1️⃣ Install **Hadoop** using Homebrew:  
   ```bash
   brew install hadoop
   ```

2️⃣ Update your shell configuration (`.zshrc` & `.bashrc`) with the following environment variables:  
   ```bash
   export HADOOP_HOME=/<enter your path>/ntr-recon-e0/hadoop
   export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/<enter your path>/ntr-recon-e0/hadoop/share/hadoop/tools/lib/*
   export PATH=$PATH:$HADOOP_HOME/bin
   export PATH=$PATH:$HADOOP_HOME/sbin
   ```

---

### 📂 Configure Hadoop Files

1️⃣ Clone the repository to local:
   ```bash
   git clone https://github.aexp.com/banan7/ntr-recon-e0
   ```

2️⃣ Open the repo and edit the Hadoop configuration file:  
   **File Path:** `ntr-e0/hadoop/etc/hadoop/hdfs-site.xml`  
   Ensure the paths match your **ntr-e0** directory:

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

   🔹 The `<value>` paths should match correctly.

---

### 🏗️ Start HDFS and YARN

1️⃣ Format the **HDFS filesystem** before first use:
   ```bash
   hdfs namenode -format -force
   ```

2️⃣ Start **HDFS** and **YARN**:
   ```bash
   start-dfs.sh && start-yarn.sh
   ```

3️⃣ Check running services:
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

4️⃣ If **NameNode** or **DataNode** do not appear in `jps`, reformat them:
   ```bash
   hdfs namenode -format  # If needed
   hdfs datanode -format  # If needed
   ```

5️⃣ If **NameNode is stuck in SafeMode**, manually exit it:
   ```bash
   hdfs dfsadmin -safemode leave
   ```

6️⃣ **Admin Access:** If required, go to **Self Service** and select **Make Me Admin**.

---

### ✅ Verify Hadoop Cluster

1️⃣ Check **HDFS NameNode UI**:
   - [http://localhost:9870](http://localhost:9870)

2️⃣ Check **YARN ResourceManager UI**:
   - [http://localhost:8088/cluster](http://localhost:8088/cluster)

---

### 🔍 Verify HDFS Functionality

1️⃣ **Create a directory in HDFS:**
   ```bash
   hdfs dfs -mkdir /ntr
   ```

2️⃣ **Put a local file into HDFS:**
   ```bash
   hdfs dfs -put ./nbachamps.txt /
   ```

3️⃣ **List HDFS contents:**
   ```bash
   hdfs dfs -ls /
   ```

---

### 🛑 Stop Hadoop Services

To stop **HDFS** and **YARN**:
   ```bash
   stop-dfs.sh && stop-yarn.sh
   ```

--- 

## 🚀 Spark Setup

1️⃣ Update your shell configuration (`.zshrc` & `.bashrc`) with the following environment variables:  
   ```bash
   export SPARK_HOME=/<your path of ntr-recon-e0 repo on local>/ntr-recon-e0/spark
   export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
   ```

2️⃣ Run `spark-shell` to verify the installation.

3️⃣ Test some commands in Spark:
   ```scala
   val txtFile = sc.textFile("hdfs://localhost/nbachamps.txt")
   val wordCount = txtFile.flatMap(line => line.split(" ")).map(word => (word,1)).reduceByKey(_ + _)
   wordCount.collect.foreach(println)
   ```

---

## 📂 Local S3 Storage (MinIO) Setup Using Docker

1️⃣ Install Docker from the **Self Service Portal**.

2️⃣ Pull the MinIO Docker image:
   ```bash
   docker pull quay.io/minio/minio
   ```

3️⃣ Verify that the MinIO image is pulled:
   ```bash
   docker images
   ```

4️⃣ Run MinIO in a Docker container:
   ```bash
   docker run -d \
       --name minio \
       -p 9000:9000 \
       -p 9090:9090 \
       -e MINIO_ROOT_USER=admin \
       -e MINIO_ROOT_PASSWORD=admin123 \
       -v ~/minio/data:/data \
       quay.io/minio/minio server /data --console-address ":9090"
   ```

5️⃣ Check if the container is running:
   ```bash
   docker ps
   ```

6️⃣ Access MinIO Web Interface:
   - URL: [http://localhost:9090](http://localhost:9090)
   - Username: `admin`
   - Password: `admin123`

7️⃣ Create a new bucket named `test-bucket` in MinIO and try uploading/deleting a file.

8️⃣ Stop and restart MinIO container:
   ```bash
   docker stop minio
   docker start minio
   ```

## 📌 HDFS Script (`hdfs_script.sh`)
This script automates the creation of necessary HDFS directories and dummy files for processing.

### 🔹 Functionality:
- Creates two directories in local HDFS:
  - `/ntr/recon/clearing/ENV_ZONE/`
  - `/ntr/clearing/ingestor/files/ENV_ZONE/`
- Deletes existing directories if present and recreates them.
- Adds dummy files to each directory (* meaning 1,2,3,etc.):
  - `dummy-recon-*.parquet`
  - `dummy-clearing-*.parquet`
- Reduces manual effort in creating and uploading parquet files to HDFS.

---

## ⚙️ Configuration Steps

### 📝 1️⃣ Update `housekeeping-configs.yml` (for S3 settings)
Modify the following parameters:
```yaml
s3_host: <your_s3_host>
s3_access_token_key: "<your_access_key>"
s3_secret_token_key: "<your_secret_key>"
bucket_name: <your_bucket_name>
```
If you change this file, upload it to HDFS:
```bash
hdfs dfs -put housekeeping-configs.yml /ntr/oozie/housekeeping/clearing/
```

### 🚀 2️⃣ Start HDFS & YARN
1. Export necessary proxies.
2. Start SSH and verify:
   ```bash
   sudo lsof -i :22
   ```
   Ensure output is displayed.
3. Start HDFS and YARN:
   ```bash
   start-dfs.sh && start-yarn.sh
   ```
4. Execute the HDFS script:
   ```bash
   ./hdfs_script.sh
   ```

### 🔥 3️⃣ Run Spark Job
Submit the Spark job using the following command:
```bash
spark-submit --master local --name test-job \
--conf spark.driver.extraJavaOptions="-DCAR_ID=600001028 -DCONNECT_TO_CONFIG_SERVER=false -DCONFIG_RELEASE_VERSION=v2024.11 -DJAR_VERSION=file-summary-audit-bnc-v2024.11.00-RELEASE.jar -DAPP_NAME=spark-warehousing -DSUB_SYSTEM_NAME=network-transaction-repository -DEPAAS_ENV_ZONE=dev -DEPAAS_ENV=e1 -DNEMO_SERVICE_NAME=spark-warehousing" \
--class com.aexp.paymentnetwork.ntr.housekeeping.Housekeeping \
/Users/akhan396/Cloned_Repo/payment-network_filesummaryaudit_bnc/spark-housekeeping/target/spark-housekeeping-1.0.jar
```

