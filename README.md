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
![image 1](https://github.com/user-attachments/assets/5681a488-fb36-4905-b10c-dfec20d4543f)
![image 2](https://github.com/user-attachments/assets/0c9724f2-49a5-4136-a388-5d960ab7c6b3)
In variable.ƞ
![Image 3](https://github.com/user-attachments/assets/d58f8ffe-826c-4d8d-b811-474ce7ae4fa2)
In output.ƞ
![Image  4](https://github.com/user-attachments/assets/7bd82136-5dca-434c-9d58-9536c99734b6)
Create a backend.ƞ file to store state file in s3 bucket
![image 5](https://github.com/user-attachments/assets/77145e5e-d3f6-445c-963f-a180e2114700)
Create a Jenkins script for terraform to run a pipeline
![image 6](https://github.com/user-attachments/assets/abf56c6b-46fe-4557-b080-fcf691e98ea3)
Explanation
pipeline: Defines a Jenkins pipeline
agent any: Runs the pipeline on any available agent
environment: Sets environment variables
AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY: Fetches AWS credenƟals stored in Jenkins
stage('Checkout'): Checks out the Terraform code from the specified Git repository
stage('Terraform Init'): IniƟalizes the Terraform configuration
stage('Terraform Format'): Checks if the Terraform files are formaƩed correctly using terraform fmt -check
stage('Terraform Validate'): Validates the Terraform configuraƟon using terraform validate
stage('Terraform Plan'): Creates an execuƟon plan using terraform plan and saves it to a file named ƞplan
stage('Terraform Apply'): Applies the changes required to reach the desired state of the configuraƟon using the previously created plan (ƞplan)
After creaƟng all files push them into git repository
git init
git remote add origin hƩps://github.com/username/repository.git
git add . # Add all fils
git commit -m "Commit message"
git push -u origin master 
use this commands to add your local files into git repository 
 open the Jenkins dashboard and select the new item
Enter an item name: terraform_cicd
Select an item type: pipeline
After selecting pipline click on ok .It opens Configuration in that select pipeline
Select pipeline script from SCM in the definition
SCM: Git
Repository URL: https://github.com/ajayguvva/terraform_cicd.git
Credentials : give your Credential
Branch Specifier: main ( branch name where the files are stored )
Script Path: jenkinsfile (path name where the script is written)
After filling all this then click on apply and save it
Now select build now and it will run cicd pipeline
This setup will provision a VPC with public and private subnets, an internet gateway, route tables, and an EC2 instance in the public subnet using Terraform. The Jenkins pipeline will automate the Terraform workﬂow from initialization to applying changes
