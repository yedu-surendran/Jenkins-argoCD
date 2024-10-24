# Lab: Install Jenkins on an Ubuntu 24.04 EC2 Instance

## Prerequisites
- **EC2 Instance**: Ubuntu 24.04 installed.
- **Security Group**: Ensure ports `8080` (Jenkins) and `22` (SSH) are open.
- **Root or sudo access**.

## Step 1: SSH into Your EC2 Instance
1. Open your terminal and connect to your EC2 instance using SSH:
    ```bash
    ssh -i <your-aws-key.pem> ubuntu@<ec2-instance-public-ip>
    ```

## Step 2: Update the System
1. Update the package lists:
    ```bash
    sudo apt update
    ```
2. Upgrade the system packages:
    ```bash
    sudo apt upgrade -y
    ```

## Step 3: Install Java
Jenkins requires Java to run. Install OpenJDK 11 (recommended version for Jenkins):
1. Install OpenJDK:
    ```bash
    sudo apt install openjdk-17-jdk -y
    ```
2. Verify Java installation:
    ```bash
    java -version
    ```

## Step 4: Add Jenkins Repository
1. Import the Jenkins GPG key:
    ```bash
    wget -O /usr/share/keyrings/jenkins-keyring.asc \
    https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
    ```
2. Add the Jenkins package repository to the system:
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    ```

## Step 5: Install Jenkins
1. Update the package list to include Jenkins:
    ```bash
    sudo apt update
    ```
2. Install Jenkins:
    ```bash
    sudo apt install jenkins -y
    ```

## Step 6: Start and Enable Jenkins
1. Start the Jenkins service:
    ```bash
    sudo systemctl enable jenkins
    ```
2. Enable Jenkins to start at boot:
    ```bash
    sudo systemctl start jenkins
    ```

## Step 7: Open Firewall for Jenkins
1. Allow port `8080` for Jenkins if UFW (Uncomplicated Firewall) is enabled:
    ```bash
    sudo ufw allow 8080
    ```
2. Check the status of UFW:
    ```bash
    sudo ufw status
    ```

## Step 8: Access Jenkins Web Interface
1. Open a browser and navigate to:
    ```
    http://<ec2-instance-public-ip>:8080
    ```

## Step 9: Unlock Jenkins
1. Retrieve the initial admin password:
    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
2. Copy the password and paste it into the Jenkins web interface to unlock Jenkins.

## Step 10: Install Suggested Plugins
1. Once logged in, select the **Install suggested plugins** option to install the recommended Jenkins plugins.

## Step 11: Create the First Admin User
1. After the plugins are installed, you will be prompted to create the first admin user. Fill in the required details and continue.

## Step 12: Jenkins is Ready
1. After completing the setup steps, Jenkins is ready to use.
2. You can now access the Jenkins dashboard at:
    ```
    http://<ec2-instance-public-ip>:8080
    ```

