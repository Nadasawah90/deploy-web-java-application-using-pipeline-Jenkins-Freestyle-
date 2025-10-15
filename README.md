# deploy-web-java-application-using-pipeline-Jenkins-Freestyle-

Freestyle Jenkins Job

A Freestyle project is the old, GUI-based way to create jobs in Jenkins as we configure everything through the Jenkins web interface (no code).

 Advantages:

Easy to use for beginners.

Quick for small, one-off jobs.

No need to write code.

🧩 Option 1 — Install Jenkins using the RHEL 9-compatible RPM manually (Recommended)

The official Jenkins repo doesn’t yet serve full systemd configs for RHEL 9.
So we’ll manually fetch the proper package and set up the missing config.

Perfect 🔥 You’re moving toward a CI/CD pipeline with Jenkins and Kubernetes (kubeadm cluster). Let’s make this step by step so it’s clear and deploys cleanly.

We’ll cover how to:
✅ Install and prepare Jenkins for pipeline builds
✅ Deploy your app to Kubernetes via Jenkins
✅ Understand difference between Freestyle and Pipeline (Jenkinsfile) in this context

Step 1. Download the latest stable Jenkins RPM
cd /tmp
sudo dnf install -y wget
wget https://pkg.jenkins.io/redhat-stable/jenkins-2.479.1-1.1.noarch.rpm


(If the version changes, you can check https://pkg.jenkins.io/redhat-stable/
 for the latest .rpm file name.)

Step 2. Install it manually
sudo dnf install -y fontconfig
sudo rpm -ivh jenkins-*.rpm

Step 3. Create the missing sysconfig file
sudo tee /etc/sysconfig/jenkins > /dev/null <<'EOF'
# Jenkins configuration for Rocky Linux 9
JENKINS_HOME="/var/lib/jenkins"
JENKINS_USER="jenkins"
JENKINS_PORT="8080"
JENKINS_LISTEN_ADDRESS="0.0.0.0"
JENKINS_ARGS="--webroot=/var/cache/jenkins/war --httpPort=${JENKINS_PORT}"
JENKINS_JAVA_CMD="/usr/bin/java"
JENKINS_JAVA_OPTIONS="-Djava.awt.headless=true -Djenkins.install.runSetupWizard=true"
PIDFILE="/var/run/jenkins.pid"
LOCKFILE="/var/lock/subsys/jenkins"
EOF

Step 4. Fix directories and permissions
sudo mkdir -p /var/lib/jenkins /var/log/jenkins /var/cache/jenkins
sudo chown -R jenkins:jenkins /var/lib/jenkins /var/log/jenkins /var/cache/jenkins

Step 5. Enable and start Jenkins
sudo systemctl daemon-reexec
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins -l


You should now see:

Jenkins is fully up and running


Check log:

sudo tail -f /var/log/jenkins/jenkins.log

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/6d8fbd98-4409-46b2-94f9-1a1a984cc69e" />

root@master01 tmp]# cat /var/lib/jenkins/secrets/initialAdminPassword

530648beaa2744bc8e8a160ebe7100b6

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/04e8213b-2e9b-4f35-af49-84600347a5ca" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/9667f4f2-5a86-463e-b3c5-314c08ce3874" />

<img width="1920" height="1030" alt="image" src="https://github.com/user-attachments/assets/b2bde272-05b4-4d99-9bc4-444ffdc9fa1b" />





