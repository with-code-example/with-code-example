---
layout: post
title: How to Use Sonarqube With Docker Compose
subtitle: Install and use sonarqube with docker
description: Docker and Docker Compose are powerful tools for containerization, allowing developers to package, distribute, and run applications and their dependencies in isolated containers.
featured_image: https://res.cloudinary.com/harendra21/image/upload/w_1200/awesome-blog/awesome-golang/How_To_Use_Soanrqube_With_Docker_Compose_c9jz7a.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/w_400/awesome-blog/awesome-golang/How_To_Use_Soanrqube_With_Docker_Compose_c9jz7a.png
tags: [golang, sonarqube]
comments: true
slug: how-to-deploy-sonarqube-with-docker-compose
date: 2023-08-05
draft: false
toc: true
series: ['Golang Sonarqube']
---

Docker and Docker Compose are powerful tools for containerization, allowing developers to package, distribute, and run applications and their dependencies in isolated containers. Here's a brief overview of both tools and instructions on how to install them on an Ubuntu machine:

## 1. Docker:
Docker is an open-source platform that enables you to create, deploy, and run applications inside containers. Containers are lightweight, portable, and self-sufficient units that include all the necessary software, libraries, and configurations required to run an application. Docker provides a consistent environment across different stages of the software development lifecycle, making it easier to build, test, and deploy applications.

Key Concepts:
- Images: A read-only template used to create containers.
- Containers: Runnable instances of images.
- Dockerfile: A text file that defines how to build a Docker image.
- Docker Hub: A public repository to share and find Docker images.

## 2. Docker Compose:
Docker Compose is a tool for defining and managing multi-container Docker applications. It allows you to use a YAML file to define the services, networks, and volumes required to run a complex application with multiple interconnected containers. Docker Compose simplifies the process of managing multiple containers and their configurations as a single cohesive application.

Key Concepts:
- `docker-compose.yml`: A YAML file that defines the services, networks, and volumes for the Docker application.
- `docker-compose up`: Command to start the application using the configuration specified in the `docker-compose.yml`.
- `docker-compose down`: Command to stop and remove the containers defined in the `docker-compose.yml`.

## Installing Docker and Docker Compose on Ubuntu:

### Step 1: Update System Packages
Open a terminal and run the following commands to update the package index and install required dependencies:

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

### Step 2: Install Docker
To install Docker, run the following commands:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

This will download and install Docker on your Ubuntu machine. After installation, add your user to the "docker" group to allow running Docker commands without using sudo:

```bash
sudo usermod -aG docker $USER
```

You will need to log out and log back in or restart your system for the group membership changes to take effect.

### Step 3: Install Docker Compose
To install Docker Compose, run the following commands:

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

This will download and install the latest version of Docker Compose on your Ubuntu machine.

### Step 4: Verify Installations
To verify that Docker and Docker Compose are installed correctly, run the following commands:

```bash
docker --version
docker-compose --version
```

You should see the respective versions of Docker and Docker Compose displayed in the terminal.

That's it! You now have Docker and Docker Compose installed on your Ubuntu machine and can start creating, managing, and deploying containerized applications.

## Install Sonarqube using docker-compose.yml

To deploy SonarQube with Docker Compose, you can use the official SonarQube Docker image from Docker Hub and set up a Docker Compose file to configure the SonarQube service. Here's a step-by-step guide to deploying SonarQube with Docker Compose:

### Step 1: Create a Docker Compose File

Create a new file named `docker-compose.yml` in your desired directory and add the following content:

```yaml
version: '3'

services:
  sonarqube:
    image: sonarqube:latest
    container_name: sonarqube
    ports:
      - "9000:9000"
    networks:
      - sonarqube_network
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_logs:/opt/sonarqube/logs
      - sonarqube_extensions:/opt/sonarqube/extensions

networks:
  sonarqube_network:

volumes:
  sonarqube_data:
  sonarqube_logs:
  sonarqube_extensions:
```

### Step 2: Deploy SonarQube with Docker Compose

Open a terminal or command prompt, navigate to the directory where you saved the `docker-compose.yml` file, and run the following command:

```bash
docker-compose up -d
```

Docker Compose will pull the latest SonarQube image from Docker Hub and start the SonarQube service in the background. The `-d` flag stands for "detached mode," which runs the services in the background.

### Step 3: Access SonarQube Web Interface

After the deployment is complete, you can access the SonarQube web interface by opening a web browser and navigating to `http://localhost:9000`. If you are running Docker on a remote server or a different port, replace `localhost` with the server's IP address or domain name and the appropriate port number.

### Step 4: Configure SonarQube

Once the SonarQube web interface is accessible, you need to complete the initial configuration:

1. Log in to SonarQube using the default credentials: `admin/admin`.

2. Change the admin password to a secure one.

3. Create a new project and obtain an authentication token for the project. You will need this token later to analyze your code.

### Step 5: Analyze Your Code

With SonarQube up and running, you can now analyze your code by integrating it with various build tools, such as Maven, Gradle, or npm. To analyze a project, you will typically need to use a SonarQube Scanner in combination with the appropriate build tool.

That's it! You now have SonarQube deployed and ready to analyze code quality in your projects using Docker Compose. Remember that for production deployments, you may want to consider additional configurations and security measures, such as SSL certificates and proper data backups.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NTYzMDAxOTBdfQ==
-->