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
 
After you login to Jenkins, - Run the command to copy the Jenkins Admin Password - 

sudo cat /var/lib/jenkins/secrets/initialAdminPassword - Enter the Administrator password

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

cd maven

./mvn -v

## 5. add maven and java to home path
cd ~

ls -a

.  ..  .bash_history  .bashrc  .lesshst  .profile  .ssh  .viminfo  .wget-hsts  snap

copy below lines to .profile file

vim .profile

#java home path

JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

export JAVA_HOME

PATH=$PATH:$JAVA_HOME/bin

export PATH

M2_HOME='/opt/apache-maven-3.9.9'

PATH="$M2_HOME/bin:$PATH"

export PATH

## 6. Setup Tomcat Server
Install Java on Tomcat server

sudo apt update

sudo apt install fontconfig openjdk-17-jre

java -version

openjdk version "17.0.8" 2023-07-18

OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb12u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb12u1, mixed mode, sharing)

Install Tomcat by copying URL from official website

![image](https://github.com/user-attachments/assets/ae5d555b-f719-4944-929c-1aef23844bc0)

https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz

cd /opt

wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.93/bin/apache-tomcat-9.0.93.tar.gz

mv apache-tomcat-9.0.93 tomcat

cd tomcat

./startup.sh

find / -name context.xml

## Issue with opening tomcay URL so Comment the lines inside the below both paths as show in screen shot.

vim /opt/tomcat/webapps/host-manager/META-INF/context.xml

 vim /opt/tomcat/webapps/manager/META-INF/context.xml

![image](https://github.com/user-attachments/assets/dd41f5f3-5ff1-4b02-b82a-f3da17be2a59)

 ./shutdown.sh
 
 ./startup.sh

Add tomcat users paddword and roles 

cd tomcat

cd conf

vim tomcat-users.xml

shift+G to go to end of the xml file

Need to add three users in tomcat-users.xml file as below,

 <role rolename="manager-gui"/>

 <role rolename="manager-script"/>
 
 <role rolename="manager-jmx"/>

 <role rolename="manager-status"/>

 <user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>

 <user username="deployer" password="deployer" roles="manager-script"/>
 
 <user username="tomcat" password="s3cret" roles="manager-gui"/>

Now login tomcat UI 

## Add tomcat credentials to jenkins

Login Jenkins --> Goto Manage Jenkins ---> Credentials ---> System ---> Click Global Credentials ---> Add Credentials as added above in tomcat-users.xml (admin, admin) 

![image](https://github.com/user-attachments/assets/c2d1deab-6ff4-452c-84f1-eb6b1dc7addb)



## 7. Install pluggins in jenkins

Login to jenkins and goto Manage Jenkins then Pluggins

Manage jenkins --> Pluggins -- Available Pluggins --> Install Maven integration pluggin and Deploy to container pluggin

![image](https://github.com/user-attachments/assets/d6b9fd74-6e19-4a36-a3a6-661a80205561)

![image](https://github.com/user-attachments/assets/22faea8d-4430-49d0-aa4b-d140bb9bd6fa)

## 8. Now Configure pluggins

Login to jenkins and goto Manage Jenkins then Tools

Manage jenkins --> Tools --> Add JDK and Maven
![image](https://github.com/user-attachments/assets/4c60af4d-ce09-4fc4-852c-e7a8e399702e)

![image](https://github.com/user-attachments/assets/8a3ab51f-733b-457b-bed6-9cee70382573)

## 9. Create New Job

Go to Dashboard --> Add New --> Select Maven

![image](https://github.com/user-attachments/assets/f663f4a6-f044-4a92-9e90-75f83a1a59a6)

Provide description of job
![image](https://github.com/user-attachments/assets/f119a441-b2a0-4a31-a42e-95d336fdf57d)

Provide git repository URL 

Note: Provide credentials of repo if repository is provite

![image](https://github.com/user-attachments/assets/e2bfa3aa-d0e9-4478-a0ed-749c05f04d74)

Provide branch name 

![image](https://github.com/user-attachments/assets/246cc9dd-d41b-440c-a6c8-0aa1126ac0ee)

Provide build options and goals

![image](https://github.com/user-attachments/assets/ceca2ec9-8329-42a4-b65d-2791bf5863a5)

Provide post build actions

Select deploy war/ear to a container --> Add Tomcat credentioals (You can add credentials under credentioals manager section ) --> Add tomcat version ex: Tomcat9 --->   Add Tomcat URL ---> apply and save


![image](https://github.com/user-attachments/assets/75838ec0-3167-413a-8657-5bbb190a1209)

## Then Finally Build the Job

![image](https://github.com/user-attachments/assets/bc1c9d92-0e06-4b17-b266-44fb22b514bf)










