## 🐳 **Docker Compose Cheat Sheet**

### 🔹 **Basic Commands**
| Command | Description |
|---------|-------------|
| `docker-compose --version` | Show installed Docker Compose version |
| `docker-compose help` | Display help for Docker Compose |

---

### 🔹 **Managing Services**
| Command | Description |
|---------|-------------|
| `docker-compose up` | Start all services defined in `docker-compose.yml` |
| `docker-compose up -d` | Start services in detached mode (background) |
| `docker-compose down` | Stop and remove all containers, networks, and volumes |
| `docker-compose stop` | Stop running containers without removing them |
| `docker-compose start` | Start previously stopped containers |
| `docker-compose restart` | Restart all services |
| `docker-compose ps` | List running services |
| `docker-compose kill` | Forcefully stop all running containers |

---

### 🔹 **Building and Rebuilding Services**
| Command | Description |
|---------|-------------|
| `docker-compose build` | Build images defined in `docker-compose.yml` |
| `docker-compose build --no-cache` | Build images without using cache |
| `docker-compose up --build` | Build and start containers in one step |

---

### 🔹 **Viewing Logs and Monitoring**
| Command | Description |
|---------|-------------|
| `docker-compose logs` | Show logs of all services |
| `docker-compose logs -f` | Follow real-time logs |
| `docker-compose logs <service>` | Show logs for a specific service |
| `docker-compose top` | Show running processes for each container |
| `docker-compose events` | Display real-time container events |

---

### 🔹 **Executing Commands in Containers**
| Command | Description |
|---------|-------------|
| `docker-compose exec <service> <command>` | Run a command inside a running container |
| `docker-compose exec <service> bash` | Open an interactive Bash shell in a container |
| `docker-compose run <service> <command>` | Run a one-time command in a new container |
| `docker-compose run --rm <service> <command>` | Run a command and remove the container after execution |

---

### 🔹 **Scaling Services**
| Command | Description |
|---------|-------------|
| `docker-compose up --scale <service>=<num>` | Scale a service to multiple instances |
| `docker-compose up -d --scale web=3` | Scale the "web" service to 3 instances |

---

### 🔹 **Managing Networks**
| Command | Description |
|---------|-------------|
| `docker-compose network ls` | List all networks created by Compose |
| `docker-compose network create <network-name>` | Create a new network |
| `docker-compose network rm <network-name>` | Remove a specific network |
| `docker-compose network inspect <network-name>` | View details of a network |

---

### 🔹 **Managing Volumes**
| Command | Description |
|---------|-------------|
| `docker-compose volume ls` | List all volumes created by Compose |
| `docker-compose volume create <volume-name>` | Create a new volume |
| `docker-compose volume rm <volume-name>` | Remove a specific volume |
| `docker-compose volume inspect <volume-name>` | View details of a volume |

---

### 🔹 **Environment and Configuration**
| Command | Description |
|---------|-------------|
| `docker-compose config` | Validate and print `docker-compose.yml` |
| `docker-compose config --services` | List services in the Compose file |
| `docker-compose config --volumes` | List volumes in the Compose file |
| `docker-compose config --images` | List images in the Compose file |

---

### 🔹 **Cleaning Up and Removing Resources**
| Command | Description |
|---------|-------------|
| `docker-compose rm` | Remove stopped services |
| `docker-compose rm -f` | Force remove stopped services |
| `docker-compose down --volumes` | Remove services and their volumes |
| `docker-compose down --rmi all` | Remove services and images |
| `docker-compose down --remove-orphans` | Remove unused containers from the project |

---

## 📌 **Most Useful Docker Compose Commands**
For a **quick reference**, here are the most commonly used commands:

```bash
docker-compose up -d              # Start all services in background
docker-compose ps                 # List running services
docker-compose logs -f             # View real-time logs
docker-compose exec <service> bash # Open a shell inside a running container
docker-compose down                # Stop and remove all services
docker-compose build               # Rebuild images
docker-compose up --scale web=3    # Scale a service to 3 instances
docker-compose restart <service>   # Restart a specific service
docker-compose down --volumes      # Remove services and associated volumes
```

---
