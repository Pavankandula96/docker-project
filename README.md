# Docker DevOps CI/CD Project

## Overview
This project demonstrates a complete CI/CD pipeline using Jenkins and Docker.

## Tech Stack
- Jenkins
- Docker
- GitHub
- Nginx

## Pipeline Flow
1. Code pushed to GitHub
2. Jenkins pulls the code
3. Docker image is built
4. Container is deployed automatically

## Project Structure
- app/ → static web files
- Dockerfile → builds nginx container
- Jenkinsfile → CI/CD pipeline

## How to Run
docker build -t myapp .
docker run -d -p 3000:80 myapp

## Output
Application runs on:
http://<your-ec2-ip>:3000
