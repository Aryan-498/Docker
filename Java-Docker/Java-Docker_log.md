# Build and Run Docker Image (Java Application)

## Objective

To build a Docker image from a Dockerfile, verify it, run a container, override commands, and understand advanced Docker concepts like layering, rebuilding, sharing images, and comparison with docker commit.

---

## Commands and Explanation

### 1. Build Image from Dockerfile

```bash
docker build -t java-app:1.0 .
```

This command builds a Docker image using the Dockerfile present in the current directory and tags it as `java-app:1.0`.

**Output:**

```bash
```

---

### 2. Verify Image

```bash
docker images
```

This command lists all locally available Docker images and verifies whether the image was created successfully.

**Output:**

```bash
```

---

### 3. Run Container from Built Image

```bash
docker run java-app:1.0
```

This command runs a container using the previously built image.

**Output:**

```bash
```

---

### 4. Override Command at Runtime

```bash
docker run -it java-app:1.0 bash
```

This command overrides the default command defined in the Dockerfile and opens an interactive bash shell inside the container.

**Output:**

```bash
```

---

## 5. Layered Build Concept

Each instruction in a Dockerfile creates a separate layer. These layers are cached and reused to improve build efficiency.

### Example Dockerfile

```dockerfile
FROM ubuntu
RUN install java
WORKDIR /home/app
COPY Hello.java
RUN javac Hello.java
CMD java Hello
```

### Explanation of Layers

* `FROM ubuntu` → Base image layer
* `RUN install java` → Installs Java
* `WORKDIR /home/app` → Sets working directory
* `COPY Hello.java` → Copies file
* `RUN javac Hello.java` → Compiles code
* `CMD java Hello` → Runs program

---

## 6. Rebuild After Code Change

After modifying `Hello.java`, rebuild the image:

```bash
docker build -t java-app:1.1 .
```

Only layers after the `COPY` instruction are rebuilt due to caching.

**Output:**

```bash
```

---

## 7. Share Dockerfile-Based Image

### Push to Registry

```bash
docker tag java-app:1.0 username/java-app:1.0
docker push username/java-app:1.0
```

This uploads your image to Docker Hub so others can access it.

**Output:**

```bash
```

---

### Pull and Run Anywhere

```bash
docker pull username/java-app:1.0
docker run username/java-app:1.0
```

This allows the image to be used on any system.

**Output:**

```bash
```

---

## 8. Dockerfile vs docker commit

| Aspect          | Dockerfile | docker commit |
| --------------- | ---------- | ------------- |
| Automation      | Yes        | No            |
| Version Control | Yes        | No            |
| CI/CD           | Yes        | No            |
| Reproducible    | Yes        | No            |
| Production Use  | Yes        | No            |

---

## 9. Key Takeaway

If it cannot be rebuilt automatically, it does not scale.

Dockerfile = Infrastructure as Code

---

## Conclusion

Docker enables efficient application deployment using layered images, reproducible builds, and easy sharing through registries. Understanding these concepts is essential for DevOps workflows.
