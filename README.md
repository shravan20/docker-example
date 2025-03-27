# Docker Example

_Deployed App on AWS-EC2 for fun_

This repository contains a simple Node.js application that has been containerized using Docker. It demonstrates how to build, run, and deploy a Dockerized app with multiple environment configurations using Docker Compose, along with CI/CD integration through Jenkins and static code analysis with SonarQube.

---

## Features

- **Containerized Application:** A Node.js server running inside a Docker container.
- **Multi-environment Support:** Separate Docker Compose files for development, staging, and production.
- **CI/CD Integration:** Automated build and deployment pipeline defined in the [Jenkinsfile](./Jenkinsfile).
- **Static Code Analysis:** SonarQube configuration provided via the `sonar-project.properties` file.

---

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- (Optional) [Jenkins](https://www.jenkins.io/) for CI/CD automation

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/shravan20/docker-example.git
cd docker-example
```

## 2. Install Dependencies

The application is built using Node.js. If you wish to install dependencies locally, run:

```
npm install
```

## 3. Running the Application with Docker

Build and run the Docker container:
```
docker build -t docker-example .
docker run -p 3000:3000 docker-example
```

The application will be accessible at http://localhost:3000.

## 4. Using Docker Compose

The repository includes multiple Docker Compose configuration files for different environments:

- Development: `docker-compose.dev.yml`
- Staging: `docker-compose.staging.yml`
- Production: `docker-compose.prod.yml`

To start the application using Docker Compose (example for development), run:

```
docker-compose -f docker-compose.dev.yml up --build
```

Replace `docker-compose.dev.yml` with the appropriate file for your target environment.


# Project Structure

```
├── Dockerfile
├── docker-compose.yml
├── docker-compose.dev.yml
├── docker-compose.staging.yml
├── docker-compose.prod.yml
├── Jenkinsfile
├── package.json
├── package-lock.json
├── server.js
├── sonar-project.properties
├── .dockerignore
└── .gitignore
```

- Dockerfile: Defines the Docker image for the Node.js application.
- docker-compose.yml:* Docker Compose files for different environments.
- server.js: The main entry point for the Node.js application.
- package.json & package-lock.json: Manage project dependencies.
- Jenkinsfile: Contains the CI/CD pipeline configuration.
- sonar-project.properties: Configuration for SonarQube static analysis.
- .dockerignore & .gitignore: Files to exclude unnecessary items from Docker builds and version control.

# Deployment

This project is designed for deployment on AWS EC2. You can:
1. Build and push your Docker images to a container registry.
2. Deploy the containers on an EC2 instance using Docker Compose.

Adjust your Docker Compose and Jenkins configurations as needed to integrate with your AWS environment.

MIT License
