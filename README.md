# SonarQube-Installation

#!/bin/bashAWS Acccount.
Create Redhat EC2 T2.medium Instance with 4GB RAM.
Create Security Group and open Required ports.
9000 ..etc
Attach Security Group to EC2 Instance.
Install java openJDK 1.8+ for SonarQube version 7.8
1. Create sonar user to manage the SonarQube server
#As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, 
# create a new user called sonar and grant sudo access to manage sonar services as follows

sudo useradd sonar
# Grand sudo access to sonar user
sudo echo "sonar ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/sonar
# set hostname for the sonarqube server
sudo hostnamectl set-hostname sonar 
sudo su - sonar
1b. Assign password to sonar user
sudo passwd sonar
2. Enable PasswordAuthentication in the server
sudo sed -i "/^[^#]*PasswordAuthentication[[:space:]]no/c\PasswordAuthentication yes" /etc/ssh/sshd_config
sudo service sshd restart
3. Install Java JDK 1.8+ required for sonarqube to start
cd /opt
sudo yum -y install unzip wget git
sudo yum install  java-11-openjdk-devel
4. Download and extract the SonarqQube Server software.
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.8.zip
sudo unzip sonarqube-7.8.zip
sudo rm -rf sonarqube-7.8.zip
sudo mv sonarqube-7.8 sonarqube
5. Grant file permissions for sonar user to start and manage sonarQube
sudo chown -R sonar:sonar /opt/sonarqube/
sudo chmod -R 775 /opt/sonarqube/
6. start sonarQube server
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start 
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh status
7. Ensure that SonarQube is running and Access sonarQube on the browser
sonarqube default port is = 9000
get the sonarqube public ip address
publicIP:9000
curl -v localhost:9000
54.236.232.85:9000
default USERNAME: admin
default password: admin
-------------------------------------------------------------------
# start sonarqube as sonar user using relative path
sudo su - sonar  
cd /opt/sonarqube/bin/linux-x86-64/ 
sh sonar.sh start
# or start sonarqube as sonar user using absolute path
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start 
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh status
#sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start | stop | status | restart
