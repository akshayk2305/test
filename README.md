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
🔑 IIQ Request & SSH Setup

📝 Raise IIQ Request

Raise an IIQ Request for your Mac with the name PRC-AXP-BA-E3-AppUser-macOS-TEMP-ADMIN from:
👉 IIQ Request Portal

Wait for approval to gain IIQ Access.

Once approved, go to Self Service and enable Make Me Admin - Engineer.

🔒 SSH Installation

Enable Make Me Admin in Self Service.

Set up proxy variables in your terminal:

export HTTP_PROXY="http://proxy.aexp.com:8080/"
export HTTPS_PROXY="https://proxy.aexp.com:8080/"

Install OpenSSH using Homebrew:

brew install openssh

Verify SSH installation:

ssh -V

✅ Expected Output:

OpenSSH_9.9p1, OpenSSL 3.4.0 22 Oct 2024

🔑 Setup SSH Key

Generate an SSH key:

ssh-keygen -t rsa -P ""

Press Enter to accept the default location and set a passphrase (optional but recommended).

Add your SSH key to authorized_keys:

cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

🔥 More setup details for Hadoop, Spark, and MinIO coming soon! Let me know if you need anything specific. 🚀

