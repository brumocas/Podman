# Podman Crash Course 🚀

Podman is a daemonless, rootless container engine that allows you to manage containers and pods without requiring root privileges. It's compatible with Docker, making the transition from Docker to Podman seamless for most users.

## Why Use Podman? 🤔
- **No Daemon**: Unlike Docker, Podman doesn't require a long-running daemon.
- **Rootless**: Podman can run containers without root privileges, improving security.
- **Docker-Compatible**: You can use Docker images and similar commands with Podman.
- **Pods**: Supports pods (like Kubernetes), allowing multiple containers to share resources.

---

## Installation

### Linux (Fedora/Ubuntu/Arch/etc.)
For **Ubuntu**:
```bash
sudo apt update
sudo apt install -y podman
```

For **Fedora**:
```bash
sudo dnf -y install podman
```

For more installation methods, check the official [Podman installation guide](https://podman.io/getting-started/installation).

---

## Basic Commands

### Pull an Image
To download a container image from a registry:
```bash
podman pull <image_name>
```
Example:
```bash
podman pull nginx:latest
```

### Run a Container
Run a container from an image:
```bash
podman run -d --name <container_name> <image_name>
```
Example:
```bash
podman run -d --name my-nginx -p 8080:80 nginx:latest
```

### List Running Containers
To see all running containers:
```bash
podman ps
```

To see all containers (including stopped ones):
```bash
podman ps -a
```

### Stop, Start, and Remove Containers
- **Stop a running container**:
  ```bash
  podman stop <container_id_or_name>
  ```

- **Start a stopped container**:
  ```bash
  podman start <container_id_or_name>
  ```

- **Remove a stopped container**:
  ```bash
  podman rm <container_id_or_name>
  ```

### Inspect a Container
To view detailed information about a container:
```bash
podman inspect <container_id_or_name>
```

### Logs
To view the logs of a container:
```bash
podman logs <container_id_or_name>
```

### Execute a Command in a Running Container
To open a shell or execute any command inside a running container:
```bash
podman exec -it <container_id_or_name> /bin/bash
```

---

## Podman vs Docker

| Feature             | Podman                                | Docker                          |
|---------------------|---------------------------------------|---------------------------------|
| **Daemon**          | Daemonless                            | Requires Docker daemon          |
| **Rootless Mode**   | Fully supports rootless containers     | Root privileges often required  |
| **Pod Support**     | Supports Pods (Kubernetes-like)        | No native pod support           |
| **Compatibility**   | Docker-compatible CLI and images      | Docker-only CLI and images      |

You can alias Docker commands to Podman for easy transitioning:
```bash
alias docker=podman
```

---

## Building Container Images

Podman can build images using a Dockerfile:

```bash
podman build -t <image_name> -f <Dockerfile>
```

Example:
```bash
podman build -t myapp:latest -f Dockerfile
```

---

## Managing Pods

Pods are groups of one or more containers that share resources. You can use pods for multi-container applications.

### Create a Pod
```bash
podman pod create --name <pod_name>
```

### Run Containers in a Pod
```bash
podman run -dt --pod <pod_name> <image_name>
```

Example:
```bash
podman pod create --name mypod
podman run -dt --pod mypod nginx
podman run -dt --pod mypod redis
```

### List Pods
```bash
podman pod ps
```

---

## Volumes and Data Persistence

Create a volume to persist data across container restarts:
```bash
podman volume create <volume_name>
```

Mount a volume to a container:
```bash
podman run -d --name <container_name> -v <volume_name>:/path/in/container <image_name>
```

Example:
```bash
podman run -d --name my-nginx -v my-volume:/usr/share/nginx/html:ro nginx
```

---

## Using Systemd with Podman

Podman can generate systemd service files to run containers as system services.

Generate a systemd unit file for a container:
```bash
podman generate systemd --name <container_name> --files --new
```

This creates a `.service` file you can move to `/etc/systemd/system` and enable as a system service:
```bash
sudo systemctl enable <container_name>.service
sudo systemctl start <container_name>.service
```

---

## Troubleshooting

- To check the status of containers, use:
  ```bash
  podman ps -a
  ```

- Check logs for troubleshooting:
  ```bash
  podman logs <container_id_or_name>
  ```

---

## Learn More

- **Official Podman Documentation**: [Podman.io](https://podman.io/)

---

This is your quick start guide to using Podman! If you’re familiar with Docker, you should find Podman easy to work with. Happy containerizing! 🎉
