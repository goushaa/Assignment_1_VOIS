# Jenkins Setup on Ubuntu Using Docker

This guide outlines the steps I followed to set up Jenkins on an Ubuntu virtual machine using Docker.

## Prerequisites

- Ubuntu VM
- Docker installed

## Steps to Set Up Jenkins

### 1. Install Docker on Ubuntu

I installed Docker by following the instructions from the official Docker documentation.

### 2. Avoid Using `sudo` with Docker Commands

Initially, I had to use `sudo` for every Docker command. To fix this, I ran the following commads:

```bash
sudo usermod -aG docker $USER
newgrp docker
```
This added my user to the Docker group, allowing me to run Docker commands without needing sudo.

### 3. Install Jenkins Using Docker

To set up Jenkins, I ran the following Docker command:

```bash
docker run -d --name kadyJenkins -v jenkins_home:/var/jenkins_home -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins:lts-jdk17
```

This command:
- Runs Jenkins in detached mode.
- Names the container "kadyJenkins."
- Maps the Jenkins home directory to a volume on the VM.
- Exposes Jenkins on port 8080 and the agent communication port on 50000.
- Ensures the container automatically restarts if it crashes.


### 4. Access Jenkins

I accessed Jenkins by navigating to `http://localhost:8080` in my web browser. 

### 5. Retrieve the Initial Admin Password

Jenkins requires an initial password, which is stored in the container at `/var/jenkins_home/secrets/initialAdminPassword`. I retrieved it using the command:

```bash
docker exec kadyJenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

### 6. Complete Jenkins Setup

I then followed the on-screen instructions in the Jenkins UI to complete the setup. Jenkins is now up and running!
