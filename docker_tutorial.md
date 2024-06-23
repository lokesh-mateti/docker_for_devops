Here's a complete tutorial for Docker, covering the basics to help you get started:

### What is Docker?

Docker is a platform that allows you to automate the deployment, scaling, and management of applications inside lightweight, portable containers. Containers package up an application and its dependencies, providing a consistent environment across different stages of development and deployment.

### Installing Docker

#### Windows and Mac

1. **Download Docker Desktop:**
   - [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)
   - [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop)

2. **Install Docker Desktop:**
   - Run the installer and follow the installation instructions.
   - After installation, Docker Desktop will start automatically.

#### Linux

1. **Install using a repository:**
   ```bash
   sudo apt-get update
   sudo apt-get install \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg-agent \
       software-properties-common

   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"

   sudo apt-get update
   sudo apt-get install docker-ce docker-ce-cli containerd.io
   ```

2. **Verify Installation:**
   ```bash
   sudo docker run hello-world
   ```

### Basic Docker Commands

#### Check Docker Version

```bash
docker --version
```

#### Pull an Image

```bash
docker pull ubuntu
```

#### List Docker Images

```bash
docker images
```

#### Run a Container

```bash
docker run -it ubuntu
```

#### List Running Containers

```bash
docker ps
```

#### List All Containers (Running + Stopped)

```bash
docker ps -a
```

#### Stop a Running Container

```bash
docker stop <container_id>
```

#### Remove a Container

```bash
docker rm <container_id>
```

#### Remove an Image

```bash
docker rmi <image_id>
```

### Building Docker Images

1. **Create a Dockerfile:**
   
   Example `Dockerfile` for a simple Node.js application:

   ```Dockerfile
   # Use an official Node runtime as a parent image
   FROM node:14

   # Set the working directory in the container
   WORKDIR /usr/src/app

   # Copy the package.json and package-lock.json
   COPY package*.json ./

   # Install dependencies
   RUN npm install

   # Copy the rest of the application
   COPY . .

   # Bind the port the app will run on
   EXPOSE 8080

   # Define the command to run the app
   CMD ["node", "app.js"]
   ```

2. **Build the Image:**
   ```bash
   docker build -t my-node-app .
   ```

3. **Run the Image:**
   ```bash
   docker run -p 8080:8080 my-node-app
   ```

### Working with Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications.

1. **Create a `docker-compose.yml` file:**

   Example `docker-compose.yml` for a simple web application with a Redis service:

   ```yaml
   version: '3'
   services:
     web:
       image: node:14
       working_dir: /usr/src/app
       volumes:
         - .:/usr/src/app
       command: npm start
       ports:
         - "8080:8080"
       depends_on:
         - redis
     redis:
       image: redis
   ```

2. **Run Docker Compose:**
   ```bash
   docker-compose up
   ```

3. **Stop Docker Compose:**
   ```bash
   docker-compose down
   ```

### Docker Networking

1. **List Networks:**
   ```bash
   docker network ls
   ```

2. **Create a Network:**
   ```bash
   docker network create my-network
   ```

3. **Connect a Container to a Network:**
   ```bash
   docker network connect my-network <container_id>
   ```

### Docker Volumes

1. **Create a Volume:**
   ```bash
   docker volume create my-volume
   ```

2. **List Volumes:**
   ```bash
   docker volume ls
   ```

3. **Mount a Volume:**
   ```bash
   docker run -v my-volume:/data -it ubuntu
   ```

### Docker Swarm

Docker Swarm is a native clustering and orchestration tool for Docker.

1. **Initialize Swarm:**
   ```bash
   docker swarm init
   ```

2. **Join a Swarm (on another machine):**
   ```bash
   docker swarm join --token <token> <manager_ip>:2377
   ```

3. **List Nodes in the Swarm:**
   ```bash
   docker node ls
   ```

4. **Deploy a Stack:**
   ```bash
   docker stack deploy -c docker-compose.yml my-stack
   ```

5. **List Services in the Stack:**
   ```bash
   docker stack services my-stack
   ```

### Cleaning Up

1. **Remove All Stopped Containers:**
   ```bash
   docker container prune
   ```

2. **Remove All Unused Images:**
   ```bash
   docker image prune
   ```

3. **Remove All Unused Networks:**
   ```bash
   docker network prune
   ```

4. **Remove All Unused Volumes:**
   ```bash
   docker volume prune
   ```

### Conclusion

This tutorial provides a solid foundation to get started with Docker. For more advanced topics, such as security practices, advanced networking, and orchestration with Kubernetes, you can refer to the [official Docker documentation](https://docs.docker.com/). Happy containerizing!
