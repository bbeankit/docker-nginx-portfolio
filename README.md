# Dockerized Web Application Deployment on AWS EC2

## Project Overview

A simple web application containerized using Docker and deployed on an AWS EC2 Ubuntu server. Nginx is used as the web server inside the Docker container, while Git and GitHub are used for source code management.

## Architecture

text
Developer
   |
   | Git Push
   v
GitHub Repository
   |
   | Git Clone
   v
AWS EC2 - Ubuntu
   |
   | Docker Build
   v
Docker Image
   |
   | Docker Run
   v
Nginx Container
   |
   | HTTP :80
   v
Internet


## Technologies Used

AWS EC2
Ubuntu Linux
Docker
Nginx
Git
GitHub
HTML
CSS

## Project Structure

docker-nginx-portfolio/
── index.html
── style.css
── Dockerfile
── README.md


## Dockerfile

The application uses the official Nginx Alpine image and copies the website files into Nginx's default web directory.

dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
COPY style.css /usr/share/nginx/html/style.css

EXPOSE 80


## Run Locally

Build the Docker image: docker build -t devops-portfolio .

Run the container: docker run -d -p 8080:80 --name devops-portfolio-container devops-portfolio

Open: http://localhost:8080


## AWS EC2 Deployment

### 1. Launch EC2
An Ubuntu EC2 instance was created on AWS.

The security group allows:

SSH - Port 22
HTTP - Port 80

### 2. Connect using SSH
ssh -i "devops-server-key.pem" ubuntu@ec2_public_ip

### 3. Clone the repository
git clone https://github.com/bbeankit/docker-nginx-portfolio
cd docker-nginx-portfolio

### 4. Build the Docker image
docker build -t devops-portfolio .


### 5. Run the container
docker run -d -p 80:80 --name devops-portfolio-container devops-portfolio

The application is then accessible through: http://ec2_public_ip


## Verification
The deployment was verified using:

docker ps

curl http://localhost

docker exec -it devops-portfolio-container nginx -v


