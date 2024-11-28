# Jenkins_Projects

Install Jenkins, configure Docker as agent, set up ci/cd, deploy applications to k8s.

## AWS EC2 Instance

- Open AWS Console
- Go to instances
- Now, Launch instance


<img width="1117" alt="111" src="https://github.com/user-attachments/assets/eaf57a90-67da-4890-9810-c4a1687b0ed6">

### Install Jenkins.

Pre-Requisites:
 - Java (JDK)

### Install Java and Jenkins

Install Java

```
sudo apt update
sudo apt install openjdk-17-jre
```

Verify, if Java is Installed

```
java -version

```

Now, proceed with installing Jenkins

```
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

**Note: ** By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules.

- Added inbound traffic rules as shown in the image (In my case, I allowed `All traffic`).

<img width="859" alt="22" src="https://github.com/user-attachments/assets/7019201f-9a96-4b48-b5e8-661da32b829a">

### Logged into Jenkins using the  URL:

http://<ec2-instance-public-ip-address>:8080    
  
After, login to Jenkins, 
      - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password

<img width="764" alt="3" src="https://github.com/user-attachments/assets/50919cf9-670b-479a-abfb-78c882a2577e">

### Click on Install suggested plugins

<img width="624" alt="4" src="https://github.com/user-attachments/assets/500125a6-f5aa-438a-bdbe-5cdf249a0f98">

Wait for the Jenkins to Install suggested plugins


<img width="746" alt="Screenshot 2024-11-28 at 1 01 05 PM" src="https://github.com/user-attachments/assets/a99699c5-34de-421f-9648-8abfe585f13f">


Create First Admin User.

<img width="771" alt="Untitled" src="https://github.com/user-attachments/assets/97640177-ce33-44b8-b36b-8b3a56d7ec58">


Jenkins Installation is Successful. 

<img width="351" alt="5" src="https://github.com/user-attachments/assets/42fa0062-39cc-4410-9422-9a9bf26f1524">


<img width="1117" alt="1" src="https://github.com/user-attachments/assets/071cd7cd-0a29-47e3-8c5c-1c8708615ac0">

## Install the Docker Pipeline plugin in Jenkins:

   - Log in to Jenkins.
   - Go to Manage Jenkins > Manage Plugins.
   - In the Available tab, search for "Docker Pipeline".
   - Select the plugin and click the Install button.
   - Restart Jenkins after the plugin is installed.
   
<img width="1121" alt="2" src="https://github.com/user-attachments/assets/2fde4555-3202-440b-a800-0ac7d4476e85">


Wait for the Jenkins to be restarted.


## Docker Slave Configuration

Run the below command to Install Docker

```
sudo apt update
sudo apt install docker.io
```
 
### Grant Jenkins user and Ubuntu user permission to docker deamon.

```
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker
```

Once you are done with the above steps, it is better to restart Jenkins.

```
http://<ec2-instance-public-ip>:8080/restart
```

The docker agent configuration is now successful.



