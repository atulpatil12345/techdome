React App with Nginx and Docker Setup

This guide outlines the steps for building and running a React app using Nginx as the web server and Docker for containerization. The app also communicates with a backend and MongoDB container over a custom Docker network.

Prerequisites
Docker installed on your machine
Basic understanding of Docker concepts (images, containers, networks)

1. Build the Frontend React App
a. Ensure nginx.conf is Present
Before building the Docker image, make sure that the nginx.conf file is present in the same directory as your Dockerfile (docker/frontend). This file configures Nginx to properly serve your React app.

b. Build the Docker Image
Navigate to the docker/frontend directory and build the React app Docker image.

cd docker/frontend
docker build -t my-react-app .

c. Run the Frontend Container
Once the image is built, run the React app container with the following command:

docker run -p 3000:80 my-react-app

Your React app will be available at http://localhost:3000 in your web browser.

2. Manual Docker Network Setup (Without Docker Compose)
In this section, we'll create a custom Docker network that allows the frontend, backend, and database containers to communicate with each other.

a. Create a Custom Docker Network
To allow communication between containers, create a custom network:

docker network create techdome-network

3. Run the MongoDB Container
Now, run the MongoDB container within the custom network:

docker pull mongo
docker run -d --network techdome-network --name mongo-db -p 27017:27017 mongo

This will start the MongoDB container, exposing port 27017 for database access.

4. Build and Run the Backend App
Navigate to the docker/backend directory, build the Docker image for the backend, and run it in the same custom network (techdome-network) so it can connect to the MongoDB container.

a. Build the Backend Docker Image
cd docker/backend
docker build -t backend-app .

b. Run the Backend Container

docker run -d --network techdome-network --name backend-app -p 5000:5000 -e DATABASE_URL=mongodb://mongo-db:27017/techdome -e PORT=5000 backend-app

This command starts the backend container and connects it to the techdome-network. It also passes the environment variable DATABASE_URL pointing to the mongo-db container.


# Apply the docker-compose file using below command
docker-compose up 
