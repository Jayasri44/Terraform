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
To access Jenkins. We need to allow inbound traffic on PORT 8080 in the AWS security group
Copy the public ip of the server and paste in the browser with port number 8080{Example : 54.89.243.242:8080} 
To unlock Jenkins we need administrator password
Go to your terminal and paste the command below to get the password to unlock Jenkins 
cat /var/lib/jenkins/secrets/iniƟalAdminPassword
Select install suggested plugins 
Create an admin user by filling in the required informaƟon
Click save and finish
Now Jenkins setup has been completed
in Jenkins dashboard select manage Jenkins and click on plugins and install terraform plugins
Now, again select manage Jenkins and click on tools and install terraform and save
Select credenƟals and add aws credenƟals and git credenƟals
Create a vpc ,public and private subnet , internet gateway ,rout table and create a ec2 
instance in public subnet by using terraform
In main.ƞ
https://github.com/Jayasri44/Terraform/issues/1#issue-2428081408
https://github.com/Jayasri44/Terraform/issues/2#issue-2428092273
In variable.ƞ
![Image 3](https://github.com/user-attachments/assets/d58f8ffe-826c-4d8d-b811-474ce7ae4fa2)
