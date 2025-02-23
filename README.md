# Project Overview:
This project entails deploying a containerized web application on an Amazon Linux EC2 instance using Docker. The workflow covers provisioning the EC2 instance, configuring necessary dependencies, containerizing the application using a Docker image built from source code, and publishing the image to Docker Hub for scalable deployment and future reuse.

Technical Description:

Provisioning and Configuration:

Launch an Amazon Linux EC2 instance.
Install essential packages, including Docker and Git.
Source Code Acquisition:

Clone the application source code from a designated GitHub repository into a working directory on the EC2 instance.
Docker Image Creation:

Author a Dockerfile to define the container environment and application dependencies.
Build a Docker image directly from the raw source code.
Container Deployment:

Run the containerized application, mapping a specific public port for external access.
Configure the appropriate AWS Security Group rules to allow inbound traffic on the designated port.
Image Publication:

Push the finalized Docker image to a repository on Docker Hub to facilitate future deployments.
Implementation Steps:

Step 1: Launch EC2 Instance and Install Dependencies

![Screenshot 2025-02-22 122357](https://github.com/user-attachments/assets/53cc4e0d-bb55-4748-83bf-175522ef53d5)

Provision an Amazon Linux EC2 instance.
Install Git and Docker using the package manager:

sudo yum update -y
sudo yum install -y git docker
sudo service docker start
sudo usermod -a -G docker ec2-user


Step 2: Clone Application Source Code

Create a working directory and clone the GitHub repository:

mkdir ~/webapp && cd ~/webapp
git clone <repository-url> .

![Screenshot 2025-02-22 122029](https://github.com/user-attachments/assets/c12d14b9-9451-49c2-9b55-19ece228beaf)

Step 3: Author Dockerfile for Containerization

Inside the working directory, create a Dockerfile:
vi Dockerfile
Add the following configuration:
dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html/

![Screenshot 2025-02-22 124039](https://github.com/user-attachments/assets/c2e4294b-0aac-4686-b63c-e53d6c083580)

Step 4: Build Docker Image

Execute the following command to build the Docker image:
docker build -t webapp_sixteenclothing .
Step 5: Deploy Docker Container

Run the container and expose it on port 8080:
docker run -d -p 8080:80 webapp_sixteenclothing
Update Security Group settings in the AWS Console to allow inbound traffic on port 8080.

![Screenshot 2025-02-22 122600](https://github.com/user-attachments/assets/9ab7fd34-d98d-4046-894c-6e71e41f4c20)

Step 6: Push Docker Image to Docker Hub

Authenticatewith Docker Hub:
docker login
Tag and push the image to your Docker Hub repository:

![Screenshot 2025-02-22 124853](https://github.com/user-attachments/assets/4d64e4c7-baee-4d12-a5b1-b6e0732924fd)

docker tag webapp_sixteenclothing <dockerhub-username>/webapp_sixteenclothing:latest
docker push <dockerhub-username>/webapp_sixteenclothing:latest

![Screenshot 2025-02-22 125604](https://github.com/user-attachments/assets/f37b69f7-a34d-44ba-86aa-e9309c508fd5)


![Screenshot 2025-02-22 124330](https://github.com/user-attachments/assets/98d6eea7-9dd6-4b7d-9c0f-bde4408f681d)

