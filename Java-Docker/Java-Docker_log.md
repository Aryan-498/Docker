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
[+] Building 91.5s (11/11) FINISHED                                                                                             docker:default
 => [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 200B                                                                                                      0.0s 
 => [internal] load metadata for docker.io/library/ubuntu:22.04                                                                           3.6s 
 => [auth] library/ubuntu:pull token for registry-1.docker.io                                                                             0.0s
 => [internal] load .dockerignore                                                                                                         0.0s
 => => transferring context: 2B                                                                                                           0.0s 
 => [1/5] FROM docker.io/library/ubuntu:22.04@sha256:3ba65aa20f86a0fad9df2b2c259c613df006b2e6d0bfcc8a146afb8c525a9751                     2.5s 
 => => resolve docker.io/library/ubuntu:22.04@sha256:3ba65aa20f86a0fad9df2b2c259c613df006b2e6d0bfcc8a146afb8c525a9751                     0.0s
 => => sha256:b1cba2e842ca52b95817f958faf99734080c78e92e43ce609cde9244867b49ed 29.54MB / 29.54MB                                          1.6s 
 => => extracting sha256:b1cba2e842ca52b95817f958faf99734080c78e92e43ce609cde9244867b49ed                                                 0.8s 
 => [internal] load build context                                                                                                         0.0s 
 => => transferring context: 182B                                                                                                         0.0s 
 => [2/5] RUN apt update && apt install -y openjdk-17-jdk                                                                                58.5s 
 => [3/5] WORKDIR /home/app                                                                                                               0.1s 
 => [4/5] COPY Hello.java .                                                                                                               0.0s 
 => [5/5] RUN javac Hello.java                                                                                                            0.8s 
 => exporting to image                                                                                                                   25.7s 
 => => exporting layers                                                                                                                  22.2s 
 => => exporting manifest sha256:fae49f47a7a20adc404eaf0cf9162a15923f3b581efcf45d233c63906d129f69                                         0.0s 
 => => exporting config sha256:652fff22a0247f781dd466ecb0827fadf5b3f48138c29b8ebd7f0b9ea59d5e42                                           0.0s 
 => => exporting attestation manifest sha256:581872ddc95a52b681d5c463e0ebabfea32ad6fc885b88f9f685b66bd1e15285                             0.0s 
 => => exporting manifest list sha256:d41bfe2a8f9c9fa8999e070c21dd0d823f62348214fa388ffe529f23df3d3d62                                    0.0s 
 => => naming to docker.io/library/java-app:1.0                                                                                           0.0s 
 => => unpacking to docker.io/library/java-app:1.0                                                                                        3.4s 
```

---

### 2. Verify Image

```bash
docker images
```

This command lists all locally available Docker images and verifies whether the image was created successfully.

**Output:**

```bash
IMAGE           ID             DISK USAGE   CONTENT SIZE   EXTRA
java-app:1.0    d41bfe2a8f9c       1.17GB          341MB
ubuntu:latest   d1e2e92c075e        119MB         31.7MB
```

---

### 3. Run Container from Built Image

```bash
docker run java-app:1.0
```

This command runs a container using the previously built image.

**Output:**

```bash
Hello from Dockerfile automation
```

---

### 4. Override Command at Runtime

```bash
docker run -it java-app:1.0 bash
```

This command overrides the default command defined in the Dockerfile and opens an interactive bash shell inside the container.

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
=> [internal] load build definition from Dockerfile                                                                                      0.0s
 => => transferring dockerfile: 144B                                                                                                      0.0s
 => WARN: JSONArgsRecommended: JSON arguments recommended for CMD to prevent unintended behavior related to OS signals (line 6)           0.0s
 => [internal] load metadata for docker.io/library/ubuntu:latest                                                                          0.0s
 => [internal] load .dockerignore                                                                                                         0.0s 
 => => transferring context: 2B                                                                                                           0.0s 
 => [1/5] FROM docker.io/library/ubuntu:latest@sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9                    0.0s 
 => => resolve docker.io/library/ubuntu:latest@sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9                    0.0s 
 => [internal] load build context                                                                                                         0.0s 
 => => transferring context: 32B  
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
The push refers to repository [docker.io/asher122498/java-app]
b1cba2e842ca: Pushed
d04be0b52c6c: Pushed
0b514486d6ee: Pushed
a4f3b388b11b: Pushed
45131a462b18: Pushed
4cbaad1e2a1a: Pushed
1.0: digest: sha256:d41bfe2a8f9c9fa8999e070c21dd0d823f62348214fa388ffe529f23df3d3d62 size: 856
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
1.0: Pulling from asher122498/java-app
Digest: sha256:d41bfe2a8f9c9fa8999e070c21dd0d823f62348214fa388ffe529f23df3d3d62
Status: Image is up to date for asher122498/java-app:1.0
docker.io/asher122498/java-app:1.0
Hello from Dockerfile automation
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
