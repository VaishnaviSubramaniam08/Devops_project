
# DevOps Project: 
🚀 Project Overview

This project demonstrates a complete DevOps pipeline for deploying applications using modern tools and cloud infrastructure. It integrates Linux, Docker, Jenkins, Nginx, AWS, and Terraform to automate build, deployment, and infrastructure provisioning.

Key Objectives:

Learn Linux command-line operations for server management.

Containerize applications using Docker.

Configure Nginx as a reverse proxy for web applications.

Implement Jenkins CI/CD pipelines to automate build and deployment.

Set up AWS EC2 instances for hosting applications.

Use Terraform to manage cloud infrastructure as code.

🛠️ Tools & Technologies

Linux Commands – File management, navigation, permissions, scripting

Docker – Containers, images, Dockerfile, Docker Compose

Nginx – Web server and reverse proxy

Jenkins – CI/CD pipelines, build & deployment automation

AWS – Account setup, EC2 instance creation, security groups

Terraform – Infrastructure provisioning and management

Git/GitHub – Version control

📂 Linux Commands Used

Some essential Linux commands used in this project:

pwd             # Print current working directory
ls -l           # List files with detailed info
cd <directory>  # Change directory
mkdir <name>    # Create directory
rm -rf <name>   # Remove file/directory
chmod +x <file> # Make script executable
nano/<editor>   # Edit files


These commands are used for server setup, script execution, and deployment tasks.

🐳 Docker Commands & Setup

Docker is used to containerize the web application.

Basic Commands:

docker --version                    # Check Docker version
docker build -t myapp:latest .      # Build Docker image
docker images                        # List Docker images
docker run -d -p 8080:80 myapp:latest  # Run container
docker ps                             # List running containers
docker stop <container_id>           # Stop a container
docker rm <container_id>             # Remove a container
docker rmi <image_id>                # Remove image


Dockerfile Example:

FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD ["node", "server.js"]

🌐 Nginx Configuration

Nginx is configured as a reverse proxy to route traffic to the Docker container.

Basic Nginx setup:

server {
    listen 80;
    server_name myapp.example.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}


Commands:

sudo apt update && sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo nginx -t       # Test configuration
sudo systemctl restart nginx

🤖 Jenkins CI/CD Pipeline

Jenkins automates build, test, and deployment.

Pipeline Steps:

Install Jenkins and required plugins.

Create a Jenkins Pipeline project.

Define pipeline using Jenkinsfile:

pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/username/myapp.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 8080:80 myapp:latest'
            }
        }
    }
}


Trigger pipelines automatically on Git push for CI/CD.

☁️ AWS Account & EC2 Setup

Steps to create and configure EC2 instance:

Create an AWS account.

Launch EC2 instance (Amazon Linux 2 or Ubuntu).

Configure security groups (allow SSH, HTTP, HTTPS).

Connect via SSH:

ssh -i "key.pem" ec2-user@<EC2-public-IP>


Install Docker, Jenkins, Nginx, and other dependencies on the EC2 instance.

🛠️ Terraform Infrastructure

Terraform automates AWS resource provisioning.

Sample Terraform Script:

provider "aws" {
  region     = "us-east-1"
  access_key = "YOUR_ACCESS_KEY"
  secret_key = "YOUR_SECRET_KEY"
}

resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "my-key"
  tags = {
    Name = "DevOps-EC2"
  }
}


Commands to run Terraform:

terraform init     # Initialize Terraform
terraform plan     # Preview changes
terraform apply    # Apply changes
terraform destroy  # Remove resources

⚡ Project Workflow

Code pushed to GitHub.

Jenkins pipeline is triggered.

Docker image is built and container is run.

Nginx routes traffic to the app container.

Infrastructure is provisioned via Terraform on AWS.
