# Dockerizing a Basic Web Application

This repository contains a basic web application that can be dockerized using Docker and Docker Compose. The web application consists of a single HTML file with associated CSS and JavaScript files.

## Steps to Dockerize the Web Application

1. Create a new directory for the Dockerize the Web Application:

    mkdir DockerizeWebApp

2. Navigate to the project directory:

    cd DockerizeWebApp

3. Create a Dockerfile:

    Create a file named **`Dockerfile`** in the root directory of the project. Open the **`Dockerfile`** and add the following content:

    ```# Use an official Nginx runtime as the base image
    ```FROM nginx:latest

    ```# Copy the application files to the appropriate location in the container
    ```COPY . /usr/share/nginx/html

    ```# Expose port 80 for the container
    ```EXPOSE 80

    ```# Start Nginx when the container launches
    ```CMD ["nginx", "-g", "daemon off;"]


4. Create a Docker Compose file:

    Create a file named **`docker-compose.yml`** in the root directory of the project. Open the file and add the following content:

    ```version: '3'
    ```services:
    ```web:
    ```    build:
    ```    context: .
    ```    dockerfile: Dockerfile
    ```    ports:
    ```    - '8080:80'
    ```    volumes:
    ```    - .:/usr/share/nginx/html
    ```    deploy:
    ```    resources:
    ```        limits:
    ```        cpus: '0.5'
    ```        memory: '512M'

5. Build and run the Docker container:

    Open a terminal or command prompt in the root directory of the project and run the following command:

    docker-compose up -d

    This command will build the Docker image using the Dockerfile and start the container based on the configuration defined in the Docker Compose file. The web application will be accessible at http://IPaddress:8080.

6. Additional Customizations (optional):

    Environment variables: To pass configuration values to the web application using environment variables, modify the Dockerfile to include the desired environment variable definitions and pass the values when running **`docker-compose up -d`**.
    Nginx configuration: To customize the Nginx configuration, create an **`nginx.conf`** file in the project directory and modify the Dockerfile to copy it to the appropriate location in the container.
    Container resource management: To limit CPU and memory usage, modify the **`docker-compose.yml`** file by adding the desired resource limits in the **`deploy`** section of the web service.
