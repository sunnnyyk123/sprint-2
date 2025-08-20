
# POC OF Java CI Checks – Static Code Analysis

## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 20-08-2025      | V1.1    |  Nitin Sharma | Internal Review | Aman Raj                 |
|                 |       | Nitin Sharma  | L0              | Shikha Tripathi        |
|                 |         | Nitin Sharma  | L1              | Kirti Nehra            |
|                 |         | Nitin Sharma  | L2              | Ashwini Singh/Deepak Nishad |


---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [System Requirements](#System-Requirements)
4. [Procedure](#procedure)
5. [Troubleshooting](#Troubleshooting)
6. [Conclusion](#conclusion)
7. [Contact Information](#contact-Information)
8. [References](#references)


---

## Introduction

This guide outlines a simple workflow to perform Static Code Analysis for Java applications using SonarQube. The goal is to ensure Go projects maintain code quality, security, and consistency throughout the development lifecycle.

---
## Prerequisites

| Dependency            | Version                   |
| --------------------- | ------------------------- |
| **Java**              | JDK 11+                   |
| **mvn**              | latest                  |
| **SonarQube**         | v9.x or above             |
| **SonarQube Scanner** | Latest compatible version |


---
## System Requirements

| Hardware/Software | Minimum Recommendation                     |
| ----------------- | ------------------------------------------ |
| **Processor**     | 2 CPU cores                                |
| **RAM**           | 4 GiB                                      |
| **Disk**          | 10 GB                                      |
| **OS**            | Ubuntu 22.04 LTS / Windows 10+ / macOS 11+ |

---


## Procedure


### Step 1: Install java and verify

```bash
sudo apt install openjdk-17-jdk -y
java -version
```

---
### Step 2: Create a SonarQube User

```bash
sudo adduser --system --no-create-home --group --disabled-login sonarqube
```
<img width="1147" height="184" alt="image" src="https://github.com/user-attachments/assets/00ca0b6a-e266-454e-920d-ea43c3ffd6ee" />

---
### Step 3: Install SonarQube

```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.90531.zip
sudo apt install unzip -y
unzip sonarqube-10.5.1.90531.zip
sudo mv sonarqube-10.5.1.90531 /opt/sonarqube
sudo chown -R sonarqube:sonarqube /opt/sonarqube

```
---
### Step 4: Create Systemd Service File

```bash
sudo nano /etc/systemd/system/sonarqube.service
```
and paste these line 

```bash
[Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking
User=sonarqube
Group=sonarqube
ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop
LimitNOFILE=65536
Restart=always

[Install]
WantedBy=multi-user.target
```
---
### Step 5: Reload, Enable & start the Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable sonarqube
sudo systemctl start sonarqube
```

---
### Step 6: Access the Dashboard

```bash
http://<INSTANCE_PUBLIC_IP>:9000
```

---

### Step 7: Create a Project in SonarQube

1. Go to **Projects** → **Create Project**  
2. Select **Manually**  
3. Enter:  
   - **Project Key** → `Java-ci-poc`  
   - **Project Name** → `Java CI POC`  
4. Choose **Locally**  
5. Generate a **Token** → copy it (we will need it in config)

---
### Step 8: Install SonarScanner

```bash
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
unzip sonar-scanner-cli-5.0.1.3006-linux.zip
sudo mv sonar-scanner-5.0.1.3006-linux /opt/sonar-scanner
echo 'export PATH=$PATH:/opt/sonar-scanner/bin' >> ~/.bashrc
source ~/.bashrc
```

and verify :

```
sonar-scanner --version
```
---

### Step 9: Clone the project repo and navigate into it

```bash
git clone <url>
cd directory
```
---
### Step 10: Configure Your Java Project

Inside your Java project root, create a file:
```
touch sonar-project.properties
```
and paste these line:

```bash
sonar.projectKey=salary-api
sonar.projectName=Salary API
sonar.projectVersion=1.0
sonar.sourceEncoding=UTF-8

# Java source code ka path
sonar.sources=src/main

# Test files ka path
sonar.tests=src/test
sonar.test.inclusions=src/test/**/*.java

# Compiled bytecode ka path (zaruri hai!)
sonar.java.binaries=target/classes

# Reports (agar baad me coverage add karna ho)
# sonar.junit.reportPaths=target/surefire-reports
# sonar.jacoco.reportPaths=target/jacoco.exec

# SonarQube server ka URL
sonar.host.url=http://3.129.209.198:9000

# Authentication token
sonar.login=sqp_c8ee5634644ff423334b14667760303e4e511306

```
---
### Step 12: Build the project using mvn

```bash
./mvnw clean install
```
<img width="1351" height="325" alt="image" src="https://github.com/user-attachments/assets/bd4cc861-19b8-4567-8d7d-1c1ca375e2a3" />

---
### Step 12: Run Analysis with SonarScanner

```
sonar-scanner
```




---
### step 13: SonarQube Web Dashboard

<img width="1346" height="554" alt="image" src="https://github.com/user-attachments/assets/d1264ecb-5fc5-4abd-8a34-4e8a46fdac5b" />

---

## Troubleshooting

| Issue                                   | Cause                                                         | Solution / Fix                                                                                                  |
| --------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **1. `sonar.sources` folder not found** | correct the folder path in `sonar.sources`   file               | Update `sonar-project.properties` with correct source directories (`.,api,client,config,...`)                   |
| **2. File indexed twice (`*_test.go`)** | Test files included in both `sonar.sources` and `sonar.tests` | Exclude test files from `sonar.sources` using `sonar.exclusions=**/*_test.go` and include them in `sonar.tests` |
| **3. Java / Scanner version issues**    | Incompatible Java version or outdated SonarScanner            | Use JDK 11+ and latest SonarScanner compatible with your SonarQube version                                      |
| **4. Scanner cache or memory issues**   | Old cache or insufficient memory                              | Clear scanner cache (`rm -rf ~/.sonar/cache`) and increase JVM memory if needed (`SONAR_SCANNER_OPTS=-Xmx512m`) |


---
##  Conclusion

Integrating static code analysis into a java CI pipeline ensures clean, secure, and maintainable code.
While multiple tools exist for linting and formatting, SonarQube should be the preferred choice because i
t goes beyond syntax checks — it provides deep code quality insights, vulnerability detection, code coverage, 
maintainability ratings, and technical debt tracking in a centralized dashboard. This not only enforces consistent
coding standards but also helps teams proactively manage risks, improve collaboration, and maintain long-term code health.

---




##  Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Nitin Sharma  | sunny.kumar.snaatak@mygurukulam.co        |

---

##  References

| Resource  | Link |
|----------|------|
| **Project Repo**  | [Visit](https://github.com/OT-MICROSERVICES/salary-api) |
| **ESLint Documentation**  | [Visit](https://eslint.org/docs/latest/) |
| **Prettier Documentation**  | [Visit](https://prettier.io/docs/en/) |
| **SonarQube Documentation** | [Visit](https://docs.sonarqube.org/latest/) |



---
