Docker for DevOps: 


This series will guide you through using Docker for common DevOps tasks, helping you streamline your workflow and achieve consistent, efficient deployments. Each post will focus on a specific task, provide step-by-step instructions with example images, and offer tips for success.

--
Part 1: 
--

**Building a Simple Web Server with Docker**
In this first post, we'll create a basic web server using a Docker image. This demonstrates the core concepts of building and running Docker containers.

What you'll learn:

Docker commands: docker pull, docker run, docker ps
Building container images from existing images
Exposing container ports

**Pull a Base Image:**

Start by pulling a pre-built image from Docker Hub. We'll use the lightweight nginx:mainline image for a web server:

*docker pull nginx:mainline (tag is up to you :))

**Run the Container:**

Use the docker run command to create and run a container based on the nginx image. We'll expose port 80 of the container to port 8080 on the host machine, allowing us to access the web server:

*docker run -d -p 8080:80 nginx:mainline

-d: Runs the container in detached mode (background)
-p 8080:80: Maps container port 80 (web server) to host port 8080

**Verify the Server:**

Open a web browser and navigate to http://localhost:8080. You should see the default Nginx welcome page.

Tip: Use docker ps to view running containers and their ports.

**Success Tip:**

This is a basic example. You can customize the container further by adding configuration files or mounting volumes for persistent data.

--
Part 2
--
Continuous Integration with Dockerfile

This post explores using a Dockerfile to automate building a container image with application dependencies. This is a key concept for continuous integration (CI) pipelines.

What you'll learn:

Dockerfile basics: instructions for building container images
Installing application dependencies
Copying application code
Step-by-Step:

**Create a Dockerfile:**

Create a file named Dockerfile in your project directory with the following content:

*********
FROM python:3.9

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python", "main.py"]
********

This Dockerfile uses the python:3.9 base image and installs dependencies from requirements.txt.
It copies your application code to the container and defines the command to run upon startup.

**Build the Image:**

Use the docker build command to build an image from your Dockerfile:

*docker build -t my-app-image .


-t my-app-image: Tags the image with the name my-app-image

Success Tip:

Integrate Dockerfile building into your CI pipeline for automated image creation with each code commit.


Par 3: 

***Multi-Container Applications with Docker Compose***

Many applications involve multiple interacting services. Docker Compose helps manage and run multi-container applications as a single unit.

What you'll learn:

Docker Compose: defining multi-container applications
Linking services within a docker-compose.yml file
Scaling services
Step-by-Step:

**Create docker-compose.yml:**

Create a file named docker-compose.yml with the following content:

***
version: "3.8"

services:
  web:
    build: .
    ports:
      - "8080:80"
  database:
    image: mysql:latest
    volumes:
      - mysql-data:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: mypassword

volumes:
  mysql-data: {}
***

This configuration defines two services: web (your application) and database (MySQL).
The ports section maps container ports to host ports.


To be continued.... :)
