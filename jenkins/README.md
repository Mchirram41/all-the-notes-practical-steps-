# Jenkins Master and Agent Setup Using SSH

This project explains how to configure Jenkins Master and Agent (Node) setup using SSH authentication in a real-time DevOps environment.

---

# Architecture

```text
Jenkins Master  ----SSH---->  Jenkins Agent(Node)
```

- Jenkins Master manages jobs and pipelines.
- Jenkins Agent executes build and deployment tasks.

---

# Prerequisites

- 2 EC2 Instances / Servers
- Security Group Ports Open:
  - 22 (SSH)
  - 8080 (Jenkins)
- Java Installed
- Internet Access

---

# Step 1: Create EC2 Instances

Create:
- Jenkins Master Server
- Jenkins Agent Server

Example OS:
- Amazon Linux 2
- Ubuntu

---

# Step 2: Install Java on Master Server

## Amazon Linux

```bash
sudo yum install java-17-amazon-corretto -y
```

## Ubuntu

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
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
sudo yum install jenkins -y
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

- Install Suggested Plugins
- Create Admin User

---

# Step 6: Install Java on Agent Server

Login to Agent server and install Java.

## Amazon Linux

```bash
sudo yum install java-17-amazon-corretto -y
```

## Ubuntu

```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
```

Verify:

```bash
java -version
```

---

# Step 7: Generate SSH Key on Master Server

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
- `id_rsa`
- `id_rsa.pub`

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

# Step 10: Verify SSH Connectivity

From Master server:

```bash
ssh ec2-user@<Agent-Public-IP>
```

or

```bash
ssh ubuntu@<Agent-Public-IP>
```

If login works without password, SSH setup is successful.

---

# Step 11: Configure Jenkins Agent

Go to:

```text
Manage Jenkins
→ Nodes
→ New Node
```

Select:
- Permanent Agent

---

# Step 12: Configure Node Details

Fill the following details:

| Field | Value |
|---|---|
| Node Name | docker-agent |
| Remote Root Directory | /home/ec2-user/jenkins |
| Labels | docker-agent |
| Usage | Use this node as much as possible |
| Launch Method | Launch agents via SSH |

---

# Step 13: Add Jenkins Credentials

Click:
```text
Add Credentials
```

Select:
- Kind → SSH Username with private key
- Username → ec2-user / ubuntu
- Private Key → Enter Directly

Get private key from Master server:

```bash
cat ~/.ssh/id_rsa
```

Copy complete private key and paste into Jenkins credentials.

Save credentials.

---

# Step 14: Launch Jenkins Agent

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

# Step 15: Use Agent in Jenkins Pipeline

Example Pipeline:

```groovy
pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage('Build') {
            steps {
                sh 'hostname'
            }
        }
    }
}
```

This pipeline runs on the Jenkins Agent node.

---

# Real-Time Best Practices

- Keep Jenkins Master lightweight.
- Execute builds on Agent nodes.
- Create separate agents for:
  - Docker
  - Kubernetes
  - Terraform
  - SonarQube
  - Maven

Example Labels:

```text
docker-agent
k8s-agent
terraform-agent
build-agent
```

---

# SSH Troubleshooting

## Permission Denied Error

Run:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Connection Timeout

Check:
- Security Group
- Port 22 open
- Public IP reachable

---

## Java Not Found

Install Java properly on Agent node.

---

# Conclusion

Successfully configured:
- Jenkins Master
- Jenkins Agent(Node)
- SSH Authentication
- Jenkins Node Integration
- Pipeline Execution on Agent Node
