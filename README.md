# Dockerized Node.js Web Application

A simple Node.js web application built with **Express.js** and containerized using **Docker**.

The main purpose of this project is to demonstrate how a basic Node.js application can be packaged into a Docker image and run consistently inside a container without depending on the local development environment.

## Project Overview

This project contains a lightweight Express.js server that serves a simple web application.

The application is packaged into a Docker container using a **Node.js 20 Alpine** base image.

### Tech Stack

* **Node.js 20**
* **Express.js 5.1.0**
* **Docker**
* **Dockerfile**
* **npm**

## Project Structure

```text
docker-project/
│
├── my-web-app/
│   ├── package.json
│   ├── package-lock.json
│   └── server.js
│
├── dockerfile
├── requirements.txt
└── README.md
```

> `requirements.txt` is not required for this Node.js project. Node.js dependencies are managed through `package.json` and `package-lock.json`.

## Prerequisites

Before running the project, make sure the following are installed on your system.

### 1. Docker

Install Docker Desktop if you're using Windows or macOS, or Docker Engine on Linux.

Verify the installation:

```bash
docker --version
```

You should get an output similar to:

```text
Docker version 28.x.x
```

### 2. Git

Git is required if you want to clone the repository.

Check whether Git is installed:

```bash
git --version
```

### 3. Node.js — Optional

Node.js is **not required** to run the application through Docker.

You only need Node.js if you want to run the application directly on your local machine without Docker.

## Clone the Repository

Clone the project using Git:

```bash
git clone https://github.com/codernj04/docker-project.git
```

Move into the project directory:

```bash
cd docker-project
```

## Build the Docker Image

Build the Docker image from the project directory:

```bash
docker build -f dockerfile -t node-docker-app .
```

### What this command does

* `docker build` — Builds a Docker image.
* `-f dockerfile` — Specifies the Dockerfile to use.
* `-t node-docker-app` — Gives the image a name.
* `.` — Uses the current directory as the build context.

You can verify that the image was created:

```bash
docker images
```

You should see:

```text
node-docker-app
```

## Run the Docker Container

Start a container from the image:

```bash
docker run -d -p 3000:3000 --name node-app-container node-docker-app
```

### Command breakdown

```text
-d
```

Runs the container in detached/background mode.

```text
-p 3000:3000
```

Maps port `3000` on your computer to port `3000` inside the container.

```text
--name node-app-container
```

Assigns a name to the running container.

```text
node-docker-app
```

Specifies the Docker image from which the container is created.

## Access the Application

Once the container is running, open your browser and visit:

```text
http://localhost:3000
```

You should see the web application served by the Express.js server.

## Check Running Containers

To see whether the application container is running:

```bash
docker ps
```

You should see something similar to:

```text
CONTAINER ID   IMAGE             PORTS
xxxxxxxxxxxx   node-docker-app   0.0.0.0:3000->3000/tcp
```

## View Application Logs

If you want to check the application output or troubleshoot an issue:

```bash
docker logs node-app-container
```

To follow the logs continuously:

```bash
docker logs -f node-app-container
```

Press `Ctrl + C` to stop following the logs.

## Stop the Container

To stop the running container:

```bash
docker stop node-app-container
```

## Start the Container Again

After stopping it, you can start the same container again:

```bash
docker start node-app-container
```

## Remove the Container

If you no longer need the container:

```bash
docker rm node-app-container
```

If the container is still running, stop it first:

```bash
docker stop node-app-container
docker rm node-app-container
```

## Remove the Docker Image

To remove the Docker image:

```bash
docker rmi node-docker-app
```

## Running Without Docker

Docker is the recommended way to run this project, but you can also run the Node.js application directly.

Go to the application directory:

```bash
cd my-web-app
```

Install the dependencies:

```bash
npm install
```

Start the application:

```bash
npm start
```

Then open:

```text
http://localhost:3000
```

## How Docker Works in This Project

The basic workflow is:

```text
Source Code
     │
     ▼
 package.json
     │
     ▼
 Dockerfile
     │
     ▼
 Docker Build
     │
     ▼
 Docker Image
     │
     ▼
 Docker Container
     │
     ▼
 Express.js Application
     │
     ▼
 localhost:3000
```

The Dockerfile creates an isolated environment containing Node.js, the application source code, and its required npm dependencies.

This means the application can run consistently on different machines without requiring the same Node.js setup on the host system.

## Useful Docker Commands

| Purpose                 | Command                                                                |
| ----------------------- | ---------------------------------------------------------------------- |
| Build image             | `docker build -f dockerfile -t node-docker-app .`                      |
| List images             | `docker images`                                                        |
| Run container           | `docker run -d -p 3000:3000 --name node-app-container node-docker-app` |
| List running containers | `docker ps`                                                            |
| List all containers     | `docker ps -a`                                                         |
| View logs               | `docker logs node-app-container`                                       |
| Stop container          | `docker stop node-app-container`                                       |
| Start container         | `docker start node-app-container`                                      |
| Remove container        | `docker rm node-app-container`                                         |
| Remove image            | `docker rmi node-docker-app`                                           |

## Troubleshooting

### Port 3000 is already in use

If port `3000` is being used by another application, map another host port:

```bash
docker run -d -p 8080:3000 --name node-app-container node-docker-app
```

Then access the application at:

```text
http://localhost:8080
```

### Check container logs

If the application isn't working as expected:

```bash
docker logs node-app-container
```

### Check whether the container is running

```bash
docker ps -a
```

## Learning Objectives

This project is mainly intended to practice:

* Creating a basic Node.js web application
* Working with Express.js
* Understanding Dockerfiles
* Building Docker images
* Running applications inside containers
* Port mapping
* Managing Docker containers
* Viewing container logs
* Understanding basic containerized application deployment

## Future Improvements

Some possible improvements for this project include:

* Add a `.dockerignore` file
* Use `npm ci` instead of `npm install` for reproducible Docker builds
* Add environment variables for configuration
* Add Docker Compose
* Add health checks
* Add a CI/CD pipeline using GitHub Actions
* Deploy the container to AWS, Azure, or another cloud platform

## Author

**Nabajyoti Mohanty**

GitHub: [@codernj04](https://github.com/codernj04)

