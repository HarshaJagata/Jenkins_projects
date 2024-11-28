# Jenkins_Projects

Install Jenkins, configure Docker as agent, set up ci/cd, deploy applications to k8s.

## AWS EC2 Instance

- Open AWS Console
- Go to instances
- Now, Launch instance

![Uploading Screenshot 2024-11-27 at 11.45.08 AM.png…]()

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

<<IMG>>

### Logged into Jenkins using the  URL:

http://<ec2-instance-public-ip-address>:8080    
  
After, login to Jenkins, 
      - Run the command to copy the Jenkins Admin Password - `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
      - Enter the Administrator password

<<IMG>>



