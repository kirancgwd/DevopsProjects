## 1. Create 2 ubuntu servers for jenkins and Tomcat in AWS
## Make Sure inbound TCP ports are enabled 80, 8080, 22, 443 in security group.

## 2. Intsall Jenkins on Jenkins server
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
  
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  
sudo apt-get update
sudo apt-get install jenkins

## 3. Install Java on Jenkins server
sudo apt update
sudo apt install fontconfig openjdk-17-jre

java -version
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

## 4. Once Jenkins and java installed Take Jenkins server IP and paste in browser
 http://IP Addrress:8080/
After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

 ![image](https://github.com/user-attachments/assets/eb2cbfd3-5019-480d-8f0c-13660b5be5be)

Click on install suggested pluggins

![image](https://github.com/user-attachments/assets/82602255-6971-4503-877c-f5808dc22a01)

Once pluggins installed create username and password

![image](https://github.com/user-attachments/assets/23d15616-5d4a-4d15-8326-53d7696e6749)

Now you can start using jenkins
![image](https://github.com/user-attachments/assets/cb593876-c728-4f0a-8b5b-a40e84c406dd)

===============Apache Maven Installation============================================================

## 4. Go to maven official website to get the donwload link.

website = https://maven.apache.org/download.cgi  ----> Copy binay tar file link
![image](https://github.com/user-attachments/assets/26429bb5-b815-4630-87e7-ca1d7c1774f9)


https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
cd /opt
wget https://dlcdn.apache.org/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.tar.gz
tar -xzvf apache-maven-3.9.9-bin.tar.gz
mv apache-maven-3.9.3 maven









## 4
