Here's a **comprehensive list of Docker commands**, grouped by categories for better readability.

---

## 🐳 **Docker Commands Cheat Sheet**

### 🔹 **Docker Basics**
| Command | Description |
|---------|-------------|
| `docker --version` | Show installed Docker version |
| `docker info` | Display system-wide information about Docker |
| `docker help` | Show help for Docker commands |

---

### 🔹 **Working with Containers**
| Command | Description |
|---------|-------------|
| `docker run <image>` | Run a container from an image |
| `docker run -d <image>` | Run container in detached mode (background) |
| `docker run -it <image> /bin/bash` | Run interactively with a shell |
| `docker run --rm <image>` | Remove container after it exits |
| `docker run --name <container-name> <image>` | Assign a custom name to the container |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running & stopped) |
| `docker stop <container>` | Stop a running container |
| `docker start <container>` | Start a stopped container |
| `docker restart <container>` | Restart a container |
| `docker kill <container>` | Force stop a container |
| `docker rm <container>` | Remove a stopped container |
| `docker rm -f <container>` | Force remove a running container |
| `docker logs <container>` | View container logs |
| `docker inspect <container>` | Get detailed information about a container |
| `docker top <container>` | Show running processes in a container |
| `docker stats <container>` | Show real-time resource usage of a container |
| `docker exec -it <container> /bin/bash` | Access a running container interactively |
| `docker cp <container>:<path> <host-path>` | Copy files from container to host |
| `docker cp <host-path> <container>:<path>` | Copy files from host to container |
| `docker rename <old-name> <new-name>` | Rename a container |

---

### 🔹 **Working with Images**
| Command | Description |
|---------|-------------|
| `docker images` | List all Docker images |
| `docker pull <image>` | Download an image from Docker Hub |
| `docker push <image>` | Upload an image to Docker Hub |
| `docker build -t <image-name> <path>` | Build an image from a Dockerfile |
| `docker commit <container> <new-image>` | Create an image from a container |
| `docker rmi <image>` | Remove an image |
| `docker image prune` | Remove unused images |

---

### 🔹 **Networking**
| Command | Description |
|---------|-------------|
| `docker network ls` | List Docker networks |
| `docker network inspect <network>` | Show details of a network |
| `docker network create <network>` | Create a custom network |
| `docker network connect <network> <container>` | Connect a container to a network |
| `docker network disconnect <network> <container>` | Disconnect a container from a network |
| `docker network rm <network>` | Remove a network |

---

### 🔹 **Volumes (Persistent Storage)**
| Command | Description |
|---------|-------------|
| `docker volume ls` | List volumes |
| `docker volume create <volume-name>` | Create a volume |
| `docker volume inspect <volume>` | Show details of a volume |
| `docker volume rm <volume>` | Remove a volume |
| `docker volume prune` | Remove all unused volumes |

---

### 🔹 **Docker Compose**
| Command | Description |
|---------|-------------|
| `docker-compose up` | Start all services in `docker-compose.yml` |
| `docker-compose up -d` | Start in detached mode (background) |
| `docker-compose down` | Stop and remove containers/networks/volumes |
| `docker-compose ps` | List running services |
| `docker-compose logs` | Show logs for all services |
| `docker-compose build` | Build images defined in `docker-compose.yml` |

---

### 🔹 **Docker Swarm (Orchestration)**
| Command | Description |
|---------|-------------|
| `docker swarm init` | Initialize a Docker Swarm |
| `docker swarm join --token <token> <manager-IP>` | Join a node to a swarm |
| `docker node ls` | List nodes in the swarm |
| `docker service create --name <service> <image>` | Deploy a service |
| `docker service ls` | List services |
| `docker service rm <service>` | Remove a service |

---

### 🔹 **Docker System Cleanup**
| Command | Description |
|---------|-------------|
| `docker system df` | Show disk usage of Docker resources |
| `docker system prune` | Remove all stopped containers, unused networks, dangling images, and build cache |
| `docker container prune` | Remove all stopped containers |
| `docker image prune` | Remove unused images |
| `docker network prune` | Remove unused networks |
| `docker volume prune` | Remove unused volumes |

---

## 📌 **Most Useful Docker Commands**


```bash
docker ps -a         # List all containers
docker images        # List images
docker run -d -p 8080:80 nginx  # Run Nginx on port 8080
docker exec -it <container> /bin/bash  # Open a shell inside a container
docker logs -f <container>  # View real-time logs
docker system prune -a  # Clean up all unused containers, networks, and images
```
