# CI/CD PIPELINE #

## Jenkins EC2 instance  ##
### Create a new EC2 instance:  ###

[http://https://www.youtube.com/watch?v=f7Isc6BdTNU&t=204s](http://https://www.youtube.com/watch?v=f7Isc6BdTNU&t=204s) 
 
- launch instances  
- Ubuntu Server 18.04 LTS (HVM), SSD Volume Type  
- t2.micro  
- default settings for "Configure Instance Details"   
- default for "Add Storage"   
- add tag (key :Name,value : Jenkins)   
- Configure Security Group: create new security group name it Jenkins, allow ssh, allow custum TCP rule, port 8080   
- create new key pair, save it  
- launch instance  

ssh to ec2 instance  
  

### Install Java   ###
[https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-18-04)   

    sudo apt update  
    apt-get install openjdk-8-jdk

**Check the java version installed**  

    java -version

In order to help Jenkins( or any Java based application) to point to the JVM (Java Virtual Machine) properly, we are required to set JAVA_HOME environment variable.

**Set JAVA_HOME:**  

` whereis javac    `   (javac: /usr/bin/javac /usr/share/man/man1/javac.1.gz) 

 `whereis java`        (java: /usr/bin/java /usr/share/java /usr/share/man/man1/java.1.gz)  
 
- Edit .bashrc and add these lines at the end

        export JAVA_HOME=/usr
        export PATH=$JAVA_HOME/bin:$PATH


### Install Jenkins ###  
[https://pkg.jenkins.io/debian-stable/](https://pkg.jenkins.io/debian-stable/)

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -  

Then add the following entry in your /etc/apt/sources.list:
    
  `deb https://pkg.jenkins.io/debian-stable binary/ ` 


Update your local package index, then finally install Jenkins:
    
      sudo apt-get update
      sudo apt-get install jenkins


**Start Jenkins**  
- You can start the Jenkins service with the command:  
 
 `sudo systemctl start jenkins`  
 
- You can enable the Jenkins service at boot with the command:  
 
 `sudo systemctl enable jenkins`    
 
- You can check the status of the Jenkins service using the command:  
 
   `sudo systemctl status jenkins ` 


**Accessing Jenkins**  

- By default jenkins runs at port 8080, You can access jenkins at

    *http://YOUR-SERVER-PUBLIC-IP:8080*
 
- Unlock Jenkins page will be shown.
 
     `cat /var/lib/jenkins/secrets/initialAdminPassword`
- Copy the key and paste it into unlock jenkins /administrator password     
- Install suggested plugins    
- create new admin user    
- save and finish    
- start jenkins  

### install git ###

[https://linuxize.com/post/how-to-install-git-on-ubuntu-18-04/](https://linuxize.com/post/how-to-install-git-on-ubuntu-18-04/)

Then set the link of git installer (/usr/bin/git) in jenkins Global Tool Configuration   

### Install docker ###
[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)


> **ERROR:** dial unix /var/run/docker.sock: connect: permission denied  
> **FIX:**  [https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket](https://www.digitalocean.com/community/questions/how-to-fix-docker-got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket)
  
    sudo usermod -aG docker ${USER}  
    sudo usermod -aG docker jenkins  
    systemctl restart docker  
    sudo chmod 666 /var/run/docker.sock ---this worked
**Add plugins:**  
Docker Pipeline

