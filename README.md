# Containers with Docker

The goals of this lab are to:
- Install [Docker](https://www.docker.com/get-started).
- Write a Dockerfile and build a Docker image.
- Run a Docker container with multiple options.
- Share your Docker container with a classmate.
- Build and run a multiple container app with docker compose.

## Useful links

- [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)

## Lab

### Resources

In the `hello-world-web-app` directory, you will find:
- A `server.js` which is the code for a simple "Hello World" [Node.js](https://nodejs.org/) web app
- A `package.json` that describes the Node.js web app and its dependencies
- A `Dockerfile` which describes the previous Node.js web app as a Docker container

## Prerequisites

Before you can start the lab, you have to:
1. Install [Docker](https://www.docker.com/get-started) following the instructions depending on your OS.
2. Make sure your docker installation in working properly by running the following command in a terminal (Cmd or Powershell for Windows):
   ```
   docker run hello-world
   ```
3. Clone the lab repository to your computer:
   ```
    git clone https://github.com/leopaul36/dsti-fall-devops-docker.git
   ```

### Lab Part 1

1. Check out the `server.js`, `package.json` and `Dockerfile` files
2. Check out the explanations for each line in the Dockerfile from [the documentation](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/#dockerfile-instructions) 
3. Build the docker container 
  1. Open a terminal (Cmd or Powershell for Windows)
  2. Navigate to the `hello-world-web-app` directory in the cloned repository
  3. Run the following command:
     ```
     docker build -t hello-world-webapp-container .
     ```
     Don't forge the `.` at the end of the command. It is here to tell Docker it should look for a Dockerfile in the current directory
     `-t` tags the built container with the name you want, here `hello-world-webapp-container`
4. Check if your Docker container appears in the local Docker images:
   ```
   docker images
   ```

### Lab Part 2

1. Run the container with the following command:
   ```
   docker run -p 12345:8080 -d hello-world-webapp-container
   ```
   1. `-p` maps a port on your local machine to a port inside the container
   2. `-d` makes the container run in background
2. Check if the container is running (and save the container ID) with the following command:
   ```
   docker ps
   ```
3. Open your web browser and go to `http://localhost:12345`
4. Print the logs of the container with:
   ```
   docker logs <container id>
   ```
3. Stop the container with:
   ```
   docker stop <container id>
   ```

### Lab Part 3

1. Modify the message printed in the `server.js` (you can add your name for example)
2. Rebuild the Docker container (with a different name) with this modified code and see if you can run it and navigate to the web app in your browser
3. Register on [Docker Hub](https://hub.docker.com/)
4. Tag your container with the following command:
   ```
   docker tag hello-world-webapp-container <docker-account-name>/<custom-image-name>
   ```
5. Push the docker image to Docker Hub:
   ```
   docker push <docker-account-name>/<custom-image-name>
   ```
6. See if you can find the image in your [repositories](https://hub.docker.com/repositories) in the Docker Hub
7. Ask a classmate to retrieve your Docker container and run it:
   ```
   docker pull <docker-account-name>/<custom-image-name>
   docker run -p 12345:8080 -d <docker-account-name>/<custom-image-name>
   ```

### Lab Part 4

1. Docker compose should be included in your Docker installation (on Windows and Mac at least), if not install it using the official [instructions](https://docs.docker.com/compose/install/)
2. Navigate to the `hello-world-compose-web-app` directory in the cloned repository
3. Build the Docker image with the name of your choice
4. Fill the missing part of the `docker-compose.yaml` file to make it use the container you just built
5. Start the containers with `docker-compose up`
6. Visit `localhost:5000` in your web browser and hit refresh a couple times
7. Stop the containers by running `CTRL+C` in the previous terminal
8. Delete the containers with:
   ```
   docker-compose rm
   ```
9. Start the containers again
   1. What happened to the counter? Why?
   2. Delete the containers again
10. Make the necessary changes in the Docker compose file so that when you delete and create the containers again the counter keeps its value

    **Hint**: Use volumes, the redis container stores its data in the /data directory

### Bonus part

1. Run Wordpress with MySQL as a Docker compose app