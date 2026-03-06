# School ERP Backend – DevOps Deployment

## Overview

This project demonstrates the containerized deployment of a backend service for a School ERP system using DevOps best practices.
The backend service exposes a REST API and is deployed using Docker. Multiple services such as the backend application, PostgreSQL database, and Redis cache are orchestrated using Docker Compose. A CI/CD pipeline is implemented using Jenkins to automate the build, test, and Docker image push process.

---

## Features

* REST API backend built using **Node.js and Express**
* Containerized application using **Docker**
* Multi-service setup using **Docker Compose**
* Database service using **PostgreSQL**
* Cache service using **Redis**
* Environment configuration using **.env**
* CI/CD pipeline using **Jenkins**
* Docker image pushed to **DockerHub**
* Health check endpoint implemented for monitoring

---

## Tech Stack

* Node.js
* Express
* PostgreSQL
* Redis
* Docker
* Docker Compose
* Jenkins
* DockerHub

---

## Project Structure

school-erp-devops
│
├── backend
│   ├── app.js
│   ├── package.json
│
├── Dockerfile
├── docker-compose.yml
├── .env
├── Jenkinsfile
└── README.md

---

## Environment Configuration

Environment variables are stored in the `.env` file.

Example configuration:

PORT=5000
DB_HOST=postgres
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME=schooldb
NODE_ENV=development

---

## Running the Project Locally

### 1. Clone the Repository

git clone https://github.com/PavanBand/school-erp-devops.git

cd school-erp-devops

---

### 2. Run the Services using Docker Compose

docker compose up --build

This command will start the following services:

* Backend API
* PostgreSQL Database
* Redis Cache

---

## API Endpoints

Main API

http://localhost:5000

Health Check Endpoint

http://localhost:5000/health

Expected Response

{"status":"OK"}

---

## Docker Image

Docker image is pushed to DockerHub.

Image name:

pavanbandi07/school-erp-devops

Pull the image:

docker pull pavanbandi07/school-erp-devops

Run the container:

docker run -p 5000:5000 pavanbandi07/school-erp-devops

---

## CI/CD Pipeline (Jenkins)

A Jenkins pipeline is used to automate the deployment process.

Pipeline stages include:

1. Clone GitHub repository
2. Install backend dependencies
3. Build Docker image
4. Run container test
5. Verify health endpoint
6. Push Docker image to DockerHub
7. Cleanup container

The pipeline configuration is defined in the **Jenkinsfile**.

---

## Author

Pavan Bandi
B.Tech CSE – AI
DevOps Enthusiast
