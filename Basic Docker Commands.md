# Docker Basic Commands

## Objective

To understand and practice commonly used Docker commands for managing images and containers.

---

## Commands and Explanation

### 1. Check Docker Version

```bash
docker version
```

This command displays detailed information about the Docker client and server versions installed on your system.

**Output:**

```bash
Client: Docker Engine - Community
 Version:           29.2.1
 API version:       1.53
 Go version:        go1.25.6
 Git commit:        a5c7197
 Built:             Mon Feb  2 17:17:26 2026
 OS/Arch:           linux/amd64
 Context:           default
```

---

### 2. Display System Information

```bash
docker info
```

This command provides system-wide information including number of containers, images, storage driver, and more.

**Output:**

```bash
```

---

### 3. List Docker Images

```bash
docker images
```

This command lists all Docker images available locally along with repository name, tag, image ID, and size.

**Output:**

```bash
```

---

### 4. Pull Ubuntu Image

```bash
docker pull ubuntu
```

This command downloads the latest Ubuntu image from Docker Hub to your local system.

**Output:**

```bash
```

---

### 5. Remove Docker Image

```bash
docker rmi ubuntu
```

This command removes the Ubuntu image from your local system.

**Output:**

```bash
```

---

### 6. Run a Container

```bash
docker run ubuntu
```

This command creates and starts a container from the Ubuntu image.

**Output:**

```bash
```

---

### 7. List Containers

```bash
docker ps
```

This command shows all currently running containers.

**Output:**

```bash
```

---

### 8. Start a Container

```bash
docker start container_name
```

This command starts an existing stopped container.

**Output:**

```bash
```

---

### 9. Stop a Container

```bash
docker stop container_name
```

This command stops a running container.

**Output:**

```bash
```

---

### 10. Restart a Container

```bash
docker restart container_name
```

This command restarts a running or stopped container.

**Output:**

```bash
```

---

### 11. Remove a Container

```bash
docker rm container_name
```

This command deletes a stopped container from the system.

**Output:**

```bash
```

---

## Conclusion

These Docker commands form the foundation for working with containers and images.
Understanding them is essential for managing containerized applications efficiently.
