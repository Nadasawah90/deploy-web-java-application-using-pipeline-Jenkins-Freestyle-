# Deploy-web-java-application-using-pipeline-Jenkins-Freestyle-manually 

We are  moving toward a CI/CD pipeline with Jenkins and Kubernetes (kubeadm cluster) to Deploymyapp to Kubernetes via Jenkins .

A Freestyle project is the old, GUI-based way to create jobs in Jenkins as we configure everything through the Jenkins web interface (no code).

### Steps : 

 1. Download the latest stable Jenkins RPM on master node or on isolated VM .

wget https://pkg.jenkins.io/redhat-stable/jenkins-2.479.1-1.1.noarch.rpm

2. Install it manually

sudo dnf install -y fontconfig

sudo rpm -ivh jenkins-*.rpm

3. Create the missing sysconfig file

sudo vi  /etc/sysconfig/jenkins 

<img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/96cec0e0-43e6-4d73-9b17-3b8dd7bb9a85" />

 4. Fix directories and permissions
 
sudo mkdir -p /var/lib/jenkins /var/log/jenkins /var/cache/jenkins

sudo chown -R jenkins:jenkins /var/lib/jenkins /var/log/jenkins /var/cache/jenkins

5. Enable and start Jenkins

sudo systemctl daemon-reexec

sudo systemctl enable jenkins

sudo systemctl start jenkins

sudo systemctl status jenkins -l

<img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/4a31f99b-ca44-482f-b0ac-8849f9c8b8d9" />


<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/6d8fbd98-4409-46b2-94f9-1a1a984cc69e" />

6- to be access jenkins webrowser should be get the admin password : 

root@master01 tmp]# cat /var/lib/jenkins/secrets/initialAdminPassword

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/04e8213b-2e9b-4f35-af49-84600347a5ca" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/9667f4f2-5a86-463e-b3c5-314c08ce3874" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/b2bde272-05b4-4d99-9bc4-444ffdc9fa1b" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/456076bc-6d31-4112-b7d2-331b6b2f08db" />

7- the first stage will be for build code as the below configuration :

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/2e88b5ba-f070-4128-a41c-13143d87537b" />

8- and the second stage to be deployed it on the kubernated as below using my repository to get yaml files for my apps   : 

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/7ee55855-655d-4373-bafd-3a8af8c67fc6" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/56c323f7-c41c-4f89-ab48-9cb1abb53538" />

9- follow the process and deployment of application : 

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/a4b47d33-b571-414f-bad4-b597df19333e" />

<img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/efcbb000-d73e-440d-a605-97bac83d7393" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/d62755ed-8b8a-4b88-a04d-4bf40812c561" />



