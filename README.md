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



