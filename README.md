RUN A CICD PIPELINE FOR TERRAFORM TO INIT,FORMAT,VALIDATE,PLAN AND APPLY
JENKINS INSTALLATION 
First install Jenkins in a server 
Create a ec2 instance and connect to that instance then switch to root user by using (sudo su –) command
Install Jekins using the commands
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \ 
 hƩps://pkg.jenkins.io/debian/jenkins.io-2023.key 
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \ 
 hƩps://pkg.jenkins.io/debian binary/ | sudo tee \ 
 /etc/apt/sources.list.d/jenkins.list > /dev/null 
sudo apt-get update 
sudo apt-get install Jenkins 
Jenkins requires java to run
install java
apt install openjdk-17-jdk -y : This command used to install java 
java -version : To check the java version 
after installing Jenkins and java in the server we need to restart the Jenkins server 
systemctl restart Jenkins : to restart the Jenkins 
systemctl status Jenkins : to check the Jenkins status , whether its running or not
LOGIN INTO JENKINS DASHBOARD 
