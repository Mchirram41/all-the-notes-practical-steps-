# Complete Jenkins DevOps Practical Guide

# What We Have Done In This Project

This README contains complete Jenkins real-time practical concepts and implementation steps.

Topics Covered:

* Jenkins Installation
* Jenkins Master and Agent Architecture
* SSH Authentication Between Master and Agent
* Jenkins Node Configuration
* Jenkins Pipeline Execution on Agent Nodes
* Jenkins Credentials Management
* Jenkins Environment Variables
* Jenkins RBAC (Role Based Access Control)
* Jenkins Webhooks with GitHub
* Jenkins Shared Libraries
* Jenkins Multibranch Pipelines
* Real-Time Best Practices
* Troubleshooting Steps
* Pipeline Examples

---

# Jenkins Master and Agent Setup Using SSH

This project explains how to configure Jenkins Master and Agent (Node) setup using SSH authentication in a real-time DevOps environment.

---

# Architecture

```text
Jenkins Master  ----SSH---->  Jenkins Agent(Node)
```

* Jenkins Master manages jobs and pipelines.
* Jenkins Agent executes build and deployment tasks.

---

# Prerequisites

* 2 EC2 Instances / Servers
* Security Group Ports Open:

  * 22 (SSH)
  * 8080 (Jenkins)
* Java Installed
* Internet Access

---

# Step 1: Create EC2 Instances

Create:

* Jenkins Master Server
* Jenkins Agent Server

Example OS:

* Amazon Linux
* Ubuntu

---

# Step 2: Install Java on Master Server

## Amazon Linux

```bash
sudo dnf install java-21-amazon-corretto -y
```

## Ubuntu

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
```

Verify Java:

```bash
java -version
```

---

# Step 3: Install Jenkins on Master Server

## Amazon Linux

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo
```

```bash
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
```

```bash
sudo dnf install jenkins -y
```

---

## Ubuntu

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

```bash
sudo apt update
sudo apt install jenkins -y
```

---

# Step 4: Start Jenkins Service

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

Check Status:

```bash
sudo systemctl status jenkins
```

---

# Step 5: Access Jenkins UI

Open browser:

```text
http://<Master-Public-IP>:8080
```

Get initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

* Install Suggested Plugins
* Create Admin User

---

# Step 6: Install Java on Agent Server

Login to Agent server and install Java.

## Amazon Linux

```bash
sudo dnf install java-21-amazon-corretto -y
```

## Ubuntu

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
```

Verify:

```bash
java -version
```

---

# Step 7: Generate SSH Key on Jenkins Master Server

Switch to Jenkins user:

```bash
sudo su - jenkins
```

Go to `.ssh` directory:

```bash
cd ~/.ssh
```

Generate SSH key:

```bash
ssh-keygen
```

Press `Enter` for all prompts.

This creates:

* `id_rsa`
* `id_rsa.pub`

---

# Step 8: Copy Public Key to Agent Server

Display public key:

```bash
cat ~/.ssh/id_rsa.pub
```

Copy the key.

Now login to Agent server:

```bash
cd ~/.ssh
```

Create `authorized_keys` file:

```bash
vi authorized_keys
```

Paste the copied public key.

Save and exit.

---

# Step 9: Give Proper Permissions

On Agent server:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

# Step 10: Create Jenkins Workspace Directory on Agent

```bash
mkdir -p /home/ec2-user/jenkins
```

Give permissions:

```bash
chmod 777 /home/ec2-user/jenkins
```

or

```bash
sudo chown -R ec2-user:ec2-user /home/ec2-user/jenkins
```

---

# Step 11: Verify SSH Connectivity

From Master server:

```bash
ssh ec2-user@<Agent-Private-IP>
```

or

```bash
ssh ubuntu@<Agent-Private-IP>
```

If login works without password, SSH setup is successful.

---

# Step 12: Create known_hosts File

Switch to Jenkins user:

```bash
sudo su - jenkins
```

Generate known_hosts entry:

```bash
ssh-keyscan -H <Agent-Private-IP> >> ~/.ssh/known_hosts
```

Set permissions:

```bash
chmod 600 ~/.ssh/known_hosts
```

---

# Step 13: Configure Jenkins Agent

Go to:

```text
Manage Jenkins
→ Nodes
→ New Node
```

Select:

* Permanent Agent

---

# Step 14: Configure Node Details

Fill the following details:

| Field                 | Value                             |
| --------------------- | --------------------------------- |
| Node Name             | docker-agent                      |
| Remote Root Directory | /home/ec2-user/jenkins            |
| Labels                | docker-agent                      |
| Usage                 | Use this node as much as possible |
| Launch Method         | Launch agents via SSH             |

---

# Step 15: Add Jenkins Credentials

Click:

```text
Add Credentials
```

Select:

* Kind → SSH Username with private key
* Username → ec2-user / ubuntu
* Private Key → Enter Directly

Get private key from Master server:

```bash
cat ~/.ssh/id_rsa
```

Copy complete private key and paste into Jenkins credentials.

Save credentials.

---

# Step 16: Launch Jenkins Agent

Click:

```text
Save
```

Jenkins connects automatically to the Agent node.

Verify under:

```text
Manage Jenkins
→ Nodes
```

Status should show:

```text
Connected
```

---

# Step 17: Use Agent in Jenkins Pipeline

Example Pipeline:

```groovy
pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo Hello World'
                sh 'hostname'
                sh 'whoami'
            }
        }
    }
}
```

This pipeline runs on the Jenkins Agent node.

---

# Jenkins Credentials Manager

## What is Jenkins Credentials Manager?

Jenkins Credentials Manager is a secure way to store:

* Passwords
* SSH Keys
* API Tokens
* Secret Files
* Certificates

Instead of hardcoding credentials inside Jenkins pipelines.

---

# Why We Use Credentials Manager

1. Hardcoding secrets in pipelines creates security risks.
2. Credentials Manager secures sensitive information.
3. It acts as centralized storage for all secrets.
4. Easy to manage and update credentials.
5. Pipelines become secure and reusable.

---

# Types of Jenkins Credentials

1. Username with Password
2. Secret Text (API Keys)
3. SSH Keys
4. Certificates
5. Secret Files

---

# Jenkins Credentials Best Practices

1. Always store secrets in Credentials Manager.
2. Never hardcode passwords or tokens.
3. Use descriptive IDs.

Example:

```text
aws-prod-key
```

4. Restrict access to credentials.
5. Rotate credentials regularly.

---

# Using Credentials in Jenkins Pipeline

Example:

```groovy
pipeline {
    agent any

    stages {
        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh 'echo $DOCKER_USER'
                }
            }
        }
    }
}
```

---

# Jenkins Environment Variables

## What are Environment Variables?

Environment variables are special variables used in Jenkins pipelines to:

* Store reusable values
* Avoid hardcoding
* Improve security
* Make pipelines flexible

Examples:

* Project Names
* Docker Tags
* Credentials
* Paths

---

# Why We Use Environment Variables

1. Store sensitive information.
2. Avoid repetitive values.
3. Change values in one place.
4. Reuse values across stages.

---

# Built-In Jenkins Environment Variables

| Variable  | Description            |
| --------- | ---------------------- |
| BUILD_ID  | Unique build number    |
| JOB_NAME  | Name of Jenkins Job    |
| WORKSPACE | Current workspace path |
| BUILD_URL | Running build URL      |

---

# Environment Variable Example

```groovy
pipeline {
    agent any

    environment {
        APP_NAME = 'my-app'
    }

    stages {
        stage('Print') {
            steps {
                sh 'echo $APP_NAME'
            }
        }
    }
}
```

---

# RBAC (Role Based Access Control)

## What is RBAC?

RBAC is a security model where permissions are assigned using roles instead of assigning permissions directly to users.

---

# Why RBAC?

1. Prevent unauthorized access.
2. Control who can:

   * View Jobs
   * Build Jobs
   * Configure Jenkins
3. Simplify permission management.

---

# RBAC Best Practices

1. Apply least privilege principle.
2. Regularly review permissions.
3. Use LDAP or Active Directory.
4. Backup Jenkins configuration.

---

# RBAC Practical Steps

## Create User

Go to:

```text
Manage Jenkins
→ Users
→ Create User
```

Create new user.

---

# Install RBAC Plugin

Install plugin:

```text
Role-based Authorization Strategy
```

Go to:

```text
Manage Jenkins
→ Plugins
```

---

# Configure RBAC

Go to:

```text
Manage Jenkins
→ Security
```

Select:

```text
Role-Based Strategy
```

Apply and Save.

---

# Assign Roles

Go to:

```text
Manage Jenkins
→ Manage and Assign Roles
```

* Create roles
* Assign permissions
* Assign users to roles

---

# Jenkins Webhooks

## What are Jenkins Webhooks?

A Git webhook is an automatic HTTP request sent from GitHub to Jenkins whenever code changes happen.

Example:

```text
Developer Pushes Code
        ↓
GitHub Webhook
        ↓
Jenkins Build Triggered Automatically
```

---

# Why We Use Webhooks

1. Enable Continuous Integration.
2. Trigger builds automatically.
3. Reduce manual work.
4. Real-time synchronization between GitHub and Jenkins.

---

# GitHub Webhook Practical Steps

Go to GitHub Repository:

```text
Settings
→ Webhooks
→ Add Webhook
```

Payload URL:

```text
http://<EC2-IP>:8080/github-webhook/
```

Content Type:

```text
application/json
```

Enable:

```text
Active
```

Save webhook.

---

# Configure Jenkins Trigger

Go to Jenkins Job:

```text
Job
→ Configure
→ Build Triggers
```

Select:

```text
GitHub hook trigger for GITScm polling
```

---

# Jenkins Shared Library

## What is Shared Library?

Shared Library is reusable Groovy code used across multiple Jenkins pipelines.

---

# Why We Use Shared Libraries

1. Reduce duplicate code.
2. Centralize common logic.
3. Easier maintenance.
4. Standardize pipelines.
5. Faster development.

---

# Shared Library Best Practices

1. Keep functions small.
2. Add proper logging.
3. Use src/ for advanced code.
4. Version the library.
5. Add README for functions.

---

# Shared Library Configuration

Go to:

```text
Manage Jenkins
→ System
→ Global Trusted Pipeline Libraries
```

Click:

```text
Add
```

Provide:

* Library Name
* Git Repository URL

---

# Jenkins Multibranch Pipeline

## What is Multibranch Pipeline?

Multibranch Pipeline automatically scans Git branches and creates separate Jenkins pipelines for each branch.

---

# Why We Use Multibranch Pipeline

1. Automatic branch discovery.
2. Automatic pipeline creation.
3. Supports feature branches.
4. Supports PR pipelines.
5. Real-time CI/CD workflows.

---

# Multibranch Pipeline Practical Steps

Go to:

```text
New Item
```

Select:

```text
Multibranch Pipeline
```

---

# Configure Branch Source

Go to:

```text
Branch Sources
→ Add Source
→ Git
```

Provide:

* Repository URL

---

# Configure Build Configuration

Mode:

```text
by Jenkinsfile
```

Script Path:

```text
Jenkinsfile
```

Apply and Save.

---

# Important Note

Each branch must contain:

```text
Jenkinsfile
```

Otherwise Jenkins cannot create pipeline for that branch.

---

# Real-Time Best Practices

* Keep Jenkins Master lightweight.
* Execute builds on agents.
* Use credentials manager.
* Avoid hardcoding.
* Use RBAC.
* Use webhooks.
* Use shared libraries.
* Use multibranch pipelines.
* Test code locally before pipelines.

---

# Common Agent Labels

```text
docker-agent
k8s-agent
terraform-agent
build-agent
```

---

# SSH Troubleshooting

## Permission Denied Error

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Connection Timeout

Check:

* Security Groups
* Port 22
* Network Access

---

## Java Not Found

Install Java on Agent.

---

## Jenkins Agent Offline

Check:

* SSH connectivity
* Credentials
* Java installation
* known_hosts

---

# Important Real-Time Notes

Before creating pipelines:

1. Build application locally.
2. Run application locally.
3. Verify dependencies.
4. Verify Docker image.
5. Then automate using Jenkins.

---

# Conclusion

Successfully configured:

* Jenkins Installation
* Jenkins Master and Agent Architecture
* SSH Authentication
* Jenkins Pipelines
* Credentials Management
* Environment Variables
* RBAC
* GitHub Webhooks
* Shared Libraries
* Multibranch Pipelines
* Real-Time Jenkins Best Practices
