WORKDIR /app    #this will be the working directory of the application inside container and when container starts by default the control will be inside this /app directory. "app" folder at root level.
COPY . . # this means copying the code from your current directory of local machine to current working directory of container( which is sprcified againt WORKDIR instructin.)

## Build Image from Docker File
==============================
Stay in the directory where Dockerfile is present
Run the command: docker build . 
OR if you have 2 dockerfile with different names i.e. Dockerfile2
docker build -f Dockerfile2

Push Image to Remote Docker Repo
===================================
# Step1: Tag the image with the repository
---------------------------------
docker tag local-image-name:tag_name dockerhub_username/repository_name:tag_name

Example: docker tag day02-todo:latest ritesh1999/cka-cert-images:latest

# Step-2: Push the image
-----------------------
Push the command with the new tag name that is associated with remote repository name.
Run the command: docker push dockerhub_username/repository_name:tag_name
Example: docker push ritesh1999/cka-cert-images:latest

## Run Container from the image that is pushed:
============================================
Now as we have pushed the image to remote repository, we can pull the image to any machine and run our application smoothly.

# Pull the docker image
--------------------
Command: docker pull dockerhub_username/repository_name:tag
Example: docker pull ritesh1999/cka-cert-images:latest

# NB: We can also pull the image to our local machine and run the container. However, as we have created the image in our local machine itself, it will not say "Image is upto date". If there is any changes to the image by some other developer then it will only download the changes.

# Run the container out of the pulled image
----------------------------------------------
Command: docker run -d --name=name_for_container -p [port] image_name
Example: docker run -d --name=todo-app -p 3000:3000 ritesh1999/cka-cert-images

-d stands for Detached mode.
-p stands for ports that needs to be exposed.
--name stands for container name. If you don't specify the name, docker will auto-assign a random name

# Container Troublshooting
---------------------------
List the container: docker ps
List all the container running/dead: docker ps -a

Access Container: docker exec -it container_name executable_name # Executable can be bash or sh based on the image
         Example: docker exec -it todo-app sh
         Once docker exec command is excuted, it will land us in the directory that was defined against WORKDIR instruction in the Dockerfie i.e. "/app" in our case.

Stop Container: docker stop container_id
Remove Container: docker rm container_id
