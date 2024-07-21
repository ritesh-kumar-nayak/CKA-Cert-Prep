## Multistage Docker Build
===========================

A multistage Docker build is a technique used to optimize Docker images by reducing their size and improving their performance. It allows you to use multiple FROM statements in a single Dockerfile, which means you can create intermediate images that are used only for building the final image. This approach helps to keep the final image smaller and cleaner because you can discard unnecessary build dependencies and artifacts.

# Dockerfile Explanation

This Dockerfile uses a multistage build to create a Docker image for a Node.js application. The process involves two stages: `Installer` and `Deployer`.

## Stage 1: Installer

### Base Image
```dockerfile
FROM node:18-alpine AS Installer

- node:18-alpine: This is a lightweight version of the Node.js image based on Alpine Linux, which is ideal for minimizing the size of the Docker image.
- AS Installer: This stage is named Installer to be referenced later in the Dockerfile.

WORKDIR /app

- WORKDIR /app: Sets the working directory inside the container to /app. All subsequent commands will be executed in this directory.

COPY package*.json ./
- COPY package*.json ./: Copies package.json and package-lock.json (if it exists) from the host machine to the working directory inside the container.

RUN npm install
- RUN npm install: Installs the dependencies listed in package.json.

COPY . .
- copying the output artifacts of "npm install" to 'this layer' only not to the container.

RUN npm run build
- RUN npm run build: Runs the build script defined in package.json, typically generating the production-ready files in a build directory.

### Stage 1: Installer

FROM nginx:latest AS Deployer
- nginx:latest: Uses the latest version of the Nginx image, a lightweight and high-performance web server.

COPY --from=Installer /app/build /usr/share/nginx/html

- COPY --from=Installer /app/build /usr/share/nginx/html: Copies only required files of built application files from the Installer stage to the Nginx web server's document root directory excluding all the other node dependacny etc.

