# E2E-CI-CD
This is a end to end CI/CD project 
Steps :
1. Initial setup and configuration

1. I am creating my servers using AWS ec2 instances with Ubuntu OS
2. Create a Jenkins Server basically a ec2 instance where we install our Jenkins(I have created a ubuntu ec2 instance)
3. Configure the security groups (make sure you opened up the 8080 port in the inbound rules because that is where we will access our Jenkins Web UI)
4. Once you are able to connect to the jenkins server we need to do two main installations
5. one is java JDK and the another is Jenkins ofcourse
6. We are installing Java JDK because jenkins is written in java and to run jenkins in our server we need to have java (make sense right?)
   but make sure you install a jenkins compatible java version either jdk 8 or 11 because java 9,10 and 12 are not compatible (at this point of time).
   I am going with jdk 11
Installing Java JDK 
 sudo apt update 
 sudo apt install openjdk-11-jdk
Installing Jenkins
 There are many ways to install Jenkins like using docker image, package managers, war files etc
 I am going with apt (no specific reason just...its very easy)
 
 curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null 
sudo apt-get update
sudo apt-get install jenkins
 
 The first command there is to check the provenance and integrity....like to make sure we are installing the legitimate jenkins application 
 because like some legend said "TRUST NO ONE" because you never know, you just installed jenkins in your server and BOOM.....your server got hacked. 
 so with the help of key rings we are authenticating that there is no harm installing this sofware into your server.
 Well the next command is basically installing jenkins.
 
 7. check jenkins status
    service jenkins status 
    If its running its ok otherwise just command jenkins not be lazy and run with the command...
    service jenkins start
 8. Access your Jenkins web ui on the port 8080 with your ec2 public ip   
 9. copy the password from the file where your jenkins initial password is present which is mostly /var/lib/jenkins/secrets/initialAdminPassword
10. paste it and login..... Hurray..... you are in...!


2. Integrate your SCM with Jenkins.

1. I am using github as my SCM
2. Install Git on Jenkins server
   Mostly the ubuntu ec2 instance comes with git installed otherwise just do
   
   sudo apt-get update
   sudo apt-get install git
   
3. Install Github plugin in Jenkins GUI
   If you have suggested plugins while setup then git will be installed otherwise just 
   
   Go to Manage Jenkins -> plugin manager -> available plugins -> git
   
4. Configure Git on Jenkins GUI
   After installing the git plugin you can see the git option in the source code management section while creating a job.
   Just select it and provide the git repo url and the credentials if it is a private repository
   That is it now create your job and that will be able to pull the code from your github repo and store it in the workspace which is /var/lib/jenkins/workspace/your job name
   
3. Integrating Maven with Jnekins

1. Setup Maven on Jenkins Server
   download maven tar.gz file and extract it
   or just run-  apt install maven
2. Setup Maven Environment variables(JAVA_HOME, M2, M2_HOME)
   If you have downloaded the tar file, you need to setup the env variables of M2 = folder where maven is instlled
   M2_HOME = maven folder/ bin, JAVA_HOME = folder where java jdk is inatslled
   
3. Install Maven plugin
   Go to Manage Jenkins -> plugin manager -> available plugins -> git
   
4. Configure Maven and Java
   go to Global tool configurations -> jdk -> give the JAVA_HOME path
   Global tool configurations -> maven -> maven home path (which you can find when you do mvn -v )
   
   
4. 

   
   
   
   
   
