## Micro-services with docker compose 

This is an explanation of the rationale behind Docker Compose configuration in setting up a simple micro-services application with a client, backend, and MongoDB service, each running in its own container. The configuration uses Docker networks to isolate communication between different parts of the application, ensuring that only necessary services can communicate with each other. Docker volumes are used to persist data, and ports are exposed to allow access from the host machine. This setup ensures a resilient and maintainable environment for deploying and running the YOLO application.


### Explanation of Configuration

#### Common Configurations across the three containers

- `restart`: always: Ensures that the services are always restarted in case of failure, improving resilience.
  
- `stdin_open`: true: Keeps the standard input open for interactive sessions, which can be useful for debugging. (better to set tty to true instead)



### Service-Specific Configurations

#### yolo-client: (this is the front logic of my app)

- `build`: Builds the Docker image for the client application from the Dockerfile located in the ./client directory.
  
- `links`: Establishes a link to the yolo-backend service, allowing the client to communicate with the backend by service name.
  
- `ports`: Maps port 3000 on the host machine to port 3000 inside the container, enabling access to the client application.
  
- `networks`: Connects to the yolo-client-backend-bridge-network for communication with the backend service.


####  yolo-backend: (this handles the routing)

- `build`: Builds the Docker image for the backend application from the Dockerfile located in the ./backend directory.

- `depends_on`: Ensures that the mongodb service is started before the backend service, maintaining the correct startup order.

- `ports`: Maps port 5000 on the host machine to port 5000 inside the container, enabling access to the backend service.

## Resulting images were published at my dockerhub registry (public mode)



- `volumes`: Mounts a Docker volume named mongodb at /var/lib/mongodb to persist MongoDB data.

- `environment`: Sets the environment variable MONGODB_URI to the MongoDB connection string.

- `networks`: Connects to both yolo-backend-mongodb-bridge-network for communication with MongoDB and yolo-client-backend-bridge-network for communication with the client.


####  mongodb:

- `image`: Specifies the Docker image to use for MongoDB (lukalmelias/yolo_mongodb:0.1.0).

- `volumes`: Mounts a Docker volume named mongodb at /var/lib/mongodb to persist MongoDB data.

- `ports`: Maps port 27017 on the host machine to port 27017 inside the container, enabling access to the MongoDB service.

- `networks`: Connects to the yolo-backend-mongodb-bridge-network for communication with the backend service.

####  Networks

`yolo-backend-mongodb-bridge-network`:

- `driver`: bridge: Creates an isolated network segment for communication between the backend and MongoDB services.

`yolo-client-backend-bridge-network`:

- `driver`: bridge: Creates an isolated network segment for communication between the client and backend services.

####  Volumes

`mongodb`: (path is left at default docker volumes)

- Defines a Docker volume to persist MongoDB data, ensuring that data is not lost when containers are stopped or removed.


![image](https://github.com/LukaLmelias/yolo/assets/71344715/5a323057-e037-400a-864e-05ef38b9f8da)


## Example tagged images

![image](https://github.com/LukaLmelias/yolo/assets/71344715/d49ea02c-3cae-4811-93aa-09a73a27c31f)

