# Docker Notes

### **Module: Introduction to Docker**

### **Containers vs Virtual Machines (VMs)**

Containers and Virtual Machines (VMs) are two widely used technologies for deploying and running applications, but they have distinct architectures, use cases, and advantages. Here's a comprehensive comparison to help understand their differences.

---

### **Overview**

| **Feature** | **Containers** | **Virtual Machines (VMs)** |
| --- | --- | --- |
| **Definition** | Lightweight, portable units for running applications and their dependencies using the host OS kernel. | Emulations of physical hardware running a full OS, each with its own kernel and resources. |
| **Architecture** | Share the host OS kernel; isolate applications at the process level. | Run a full guest OS, including the kernel, on top of a hypervisor. |
| **Performance** | High performance due to lightweight nature and minimal overhead. | Slower compared to containers due to overhead from running a full OS. |
| **Portability** | Highly portable across different environments (e.g., local, cloud, on-premise). | Portable but more challenging to migrate due to larger disk and memory footprints. |
| **Startup Time** | Milliseconds (since containers don't boot a full OS). | Minutes (a full OS boot is required). |
| **Resource Utilization** | Efficient and lightweight; can run many containers on a single machine. | Heavier; each VM consumes a significant amount of memory and CPU for the guest OS. |
| **Isolation** | Process-level isolation; not as secure as VMs since they share the same kernel. | Stronger isolation because each VM runs its own OS and kernel. |
| **Use Cases** | Microservices, rapid development, testing, scaling, and cloud-native applications. | Running multiple OS environments, legacy applications, and workloads requiring strict isolation. |

---

### **Architectural Differences**

### **Containers**

1. **How They Work**:
    - Containers virtualize the **operating system**, not the hardware.
    - Applications share the **host OS kernel**, and each container runs as an isolated user-space process.
2. **Key Components**:
    - **Container Engine**: Software like Docker, Kubernetes, or Podman manages container lifecycle and orchestration.
    - **Images**: Containers are built from images that include the application and its dependencies.
    - **Isolation**: Achieved using features like cgroups (control groups) and namespaces.
3. **Advantages**:
    - Lightweight and fast.
    - Ideal for **microservices architecture**.
    - Simplified deployment and consistent environments.
    - Seamless integration with CI/CD pipelines.
4. **Disadvantages**:
    - Security risks due to shared kernel.
    - Limited support for non-Linux operating systems (although tools like WSL2 help bridge the gap).

### **Virtual Machines**

1. **How They Work**:
    - VMs virtualize the **hardware**, providing an abstraction layer where a guest OS operates as if it were on physical hardware.
    - A **hypervisor** (e.g., VMware, VirtualBox, Hyper-V, KVM) manages the VMs.
2. **Key Components**:
    - **Hypervisor**: Software layer that virtualizes hardware for guest OS.
    - **Guest OS**: Each VM runs a complete OS instance, independent of the host OS.
    - **VM Image**: Includes the OS, application, and dependencies.
3. **Advantages**:
    - Strong isolation, as each VM runs its own OS and kernel.
    - Can run multiple operating systems (e.g., Linux and Windows on the same host).
    - Well-suited for legacy applications that require specific OS environments.
4. **Disadvantages**:
    - Higher overhead due to full OS instances.
    - Slower startup and resource-intensive.
    - Requires significant storage and memory resources.

---

### **When to Use Containers vs VMs**

### **Use Containers When**:

- Building **cloud-native applications** (e.g., microservices).
- Rapidly deploying, scaling, or testing applications.
- Running multiple instances of the same application.
- You need lightweight, portable environments.

### **Use Virtual Machines When**:

- You need to run multiple operating systems on the same hardware.
- Your workload demands strong isolation and strict security.
- Running legacy applications or software requiring specific OS versions.
- Building and testing infrastructure-level systems.

---

### **Containerization**

**Containerization** is a lightweight virtualization method that packages an application and its dependencies into a single, portable unit called a **container**. Containers ensure that an application runs consistently across different environments, such as development, testing, and production.

---

### **Key Features of Containerization**

1. **Lightweight**:
    - Containers share the host operating system's kernel, making them significantly smaller and faster than virtual machines.
    - They include only the necessary libraries, dependencies, and configurations for the application.
2. **Portable**:
    - Containers are platform-agnostic. A containerized application can run consistently on any system that supports the container runtime (e.g., Docker Engine).
    - This eliminates the "works on my machine" problem.
3. **Isolated**:
    - Each container runs in its own isolated user space, ensuring that processes inside one container do not interfere with others.
    - Isolation is achieved using features like **Linux namespaces** and **cgroups**.
4. **Efficient Resource Utilization**:
    - Containers use the underlying host OS, avoiding the overhead of a full guest OS.
    - Multiple containers can run on a single host efficiently, enabling high density.
5. **Immutable and Versioned**:
    - Containers are built from **images**, which are version-controlled and immutable.
    - Updates are applied by creating a new image, ensuring consistent deployment.
6. **Rapid Deployment and Scalability**:
    - Containers can be started in milliseconds, enabling rapid scaling of applications.
    - Tools like Kubernetes facilitate automatic scaling and orchestration of containers.

---

### **How Does Containerization Work?**

1. **Container Images**:
    - A container image is a lightweight, standalone, and executable package that includes everything needed to run an application: code, runtime, libraries, and configurations.
    - Images are built using a **Dockerfile** (or similar tool) and stored in **container registries** (e.g., Docker Hub, Amazon ECR).
2. **Container Runtime**:
    - The runtime (e.g., Docker Engine, containerd) manages containers on the host system. It starts, stops, and manages containers by leveraging features of the host OS kernel.
3. **Container Orchestration**:
    - In production environments, orchestration tools like **Kubernetes**, **Docker Swarm**, or **Red Hat OpenShift** manage the deployment, scaling, and networking of containers.

---

### **Key Benefits of Containerization**

1. **Consistency Across Environments**:
    - Containers bundle all dependencies, ensuring that applications behave the same way across different systems.
2. **Speed and Efficiency**:
    - Fast startup times and lightweight nature allow for quick development, testing, and deployment cycles.
    - Containers consume fewer resources compared to virtual machines.
3. **Scalability**:
    - Containers can be scaled horizontally by running multiple instances of the same containerized application.
    - Modern orchestration tools allow automatic scaling based on demand.
4. **Improved CI/CD Pipelines**:
    - Containerization simplifies the build, test, and deployment processes by providing a consistent runtime environment.
5. **Microservices Support**:
    - Containers are ideal for microservices architectures, where each service can run independently in its container.

---

### **Containerization Workflow**

1. **Build**:
    - Developers create a **Dockerfile** (or similar file) to define the environment, dependencies, and instructions for running the application.
    - A container image is built using this Dockerfile.
2. **Test**:
    - The container image is tested in a local or staging environment to verify functionality.
3. **Deploy**:
    - The image is pushed to a container registry (e.g., Docker Hub).
    - The image is pulled from the registry and deployed to production.
4. **Run**:
    - The containerized application is run on the target environment using the container runtime.

---

### **Use Cases of Containerization**

1. **Microservices Architecture**:
    - Run each microservice in its own container for independent deployment and scaling.
2. **Continuous Integration/Continuous Deployment (CI/CD)**:
    - Containers provide consistent environments for building, testing, and deploying code.
3. **Cloud-Native Applications**:
    - Containers are the foundation of cloud-native development and deployment practices.
4. **Legacy Application Modernization**:
    - Containerizing legacy applications allows them to run in modern environments without significant code changes.
5. **Multi-Tenant Applications**:
    - Containers enable resource isolation, making them ideal for multi-tenant architectures.

---

### **Comparison of Containerization with Virtualization**

| **Aspect** | **Containers** | **Virtual Machines (VMs)** |
| --- | --- | --- |
| **Performance** | Lightweight, fast startup | Heavyweight, slower startup |
| **Isolation** | Process-level isolation | Full OS-level isolation |
| **Resource Utilization** | Highly efficient | Higher resource overhead |
| **Portability** | Highly portable | Portable, but requires matching hypervisors |
| **Use Cases** | Microservices, cloud-native apps, CI/CD | Legacy apps, OS-specific requirements |

---

### **Docker Architecture**

Docker is a platform designed to simplify the process of creating, deploying, and running applications using **containers**. Its architecture is modular and efficient, consisting of several components that work together to manage containerized applications. Here’s an in-depth overview of Docker's architecture:

---

### **Key Components of Docker Architecture**

1. **Docker Engine**
    
    The Docker Engine is the core of the Docker platform, responsible for running and managing containers. It has three main components:
    
    - **Docker Daemon (dockerd)**:
        - A server that listens for Docker API requests and manages objects like images, containers, networks, and volumes.
        - Runs as a background process on the host machine.
    - **Docker CLI (Command-Line Interface)**:
        - A command-line tool that allows users to interact with Docker.
        - Commands like `docker run`, `docker build`, and `docker pull` communicate with the Docker daemon.
    - **REST API**:
        - Provides a programmatic interface for interacting with the Docker daemon.
        - Enables integration with custom tools or remote management.
2. **Docker Objects**
    
    Docker uses several objects to manage and run containers:
    
    - **Images**:
        - Immutable, read-only templates that include an application and its dependencies.
        - Built using a **Dockerfile** and stored in registries.
    - **Containers**:
        - Running instances of Docker images.
        - Containers are lightweight and isolated, sharing the host OS kernel.
    - **Volumes**:
        - Persistent storage solutions for containers, separate from the container's lifecycle.
    - **Networks**:
        - Facilitate communication between containers or between containers and the host.
3. **Docker Registries**
    - Repositories for storing and distributing Docker images.
    - Popular registries include **Docker Hub**, **Amazon Elastic Container Registry (ECR)**, **Google Container Registry (GCR)**, and **Azure Container Registry (ACR)**.
    - Docker images are pulled from registries when running containers (`docker pull`) and pushed to registries when sharing images (`docker push`).

---

### **Workflow of Docker Architecture**

1. **Building an Image**:
    - A developer writes a **Dockerfile**, defining the base image, dependencies, and application instructions.
    - The Docker CLI issues a `docker build` command, which the Docker daemon processes to create an image.
2. **Running a Container**:
    - The user issues a `docker run` command through the CLI.
    - The Docker daemon pulls the requested image (if not available locally) from the registry and creates a container instance.
    - The container is launched with the specified configuration (e.g., ports, volumes, environment variables).
3. **Managing Containers**:
    - The Docker CLI provides commands to list, stop, start, or remove containers.
    - The Docker daemon handles the container’s lifecycle, monitoring its state and resource usage.

---

### **Detailed Diagram of Docker Architecture**

```
+----------------------------+         +-------------------------------+
|        Docker CLI          |  --->  |           REST API            |
+----------------------------+         +-------------------------------+
                   |                                  |
                   |                                  |
                   v                                  v
       +-----------------------------+   +------------------------------+
       |       Docker Daemon         |   |      Container Registry      |
       |  (dockerd)                  |   |  (e.g., Docker Hub)          |
       +-----------------------------+   +------------------------------+
                   |                                  ^
                   v                                  |
+------------------------------------+               |
|          Docker Objects           |<---------------+
|  (Images, Containers, Networks,   |
|   Volumes)                        |
+------------------------------------+

```

---

### **Advantages of Docker Architecture**

1. **Lightweight and Efficient**:
    - Containers share the host OS kernel, reducing resource overhead.
2. **Portability**:
    - Applications run consistently across different environments (local, staging, production).
3. **Modularity**:
    - Each component of Docker is modular and can be managed independently.
4. **Ease of Use**:
    - Simplifies application deployment with a consistent workflow.
5. **Integration with Orchestration Tools**:
    - Works seamlessly with tools like Kubernetes for scaling and managing containers in production.

---

### **Module: Docker Installation and Setup**

### **Installing Docker**

Docker can be installed on various operating systems, including **Windows**, **macOS**, and **Linux**. The installation process varies slightly depending on your platform. Below are step-by-step instructions for installing Docker on the most common environments.

---

### **1. Install Docker on Windows**

### **Prerequisites**:

- Windows 10 or 11 (64-bit) Pro, Enterprise, or Education with **Hyper-V** enabled.
- Windows Home edition requires **Windows Subsystem for Linux 2 (WSL 2)**.

### **Steps**:

1. **Download Docker Desktop**:
    - Visit the [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/) page and download the installer.
2. **Install Docker Desktop**:
    - Run the downloaded `.exe` file and follow the on-screen instructions.
    - During installation, enable the option to install **Windows Subsystem for Linux 2** (if not already installed).
    - Ensure **Hyper-V** is enabled (Docker installer will handle this automatically if required).
3. **Start Docker Desktop**:
    - Launch Docker Desktop from the Start menu.
    - Complete the setup by signing in or creating a Docker Hub account.
4. **Verify Installation**:
    - Open a terminal or PowerShell and run:
        
        ```bash
        docker --version
        
        ```
        
    - You should see the installed Docker version.

---

### **2. Install Docker on macOS**

### **Prerequisites**:

- macOS 10.15 (Catalina) or later.
- Apple Silicon (M1/M2) or Intel chip.

### **Steps**:

1. **Download Docker Desktop**:
    - Visit the [Docker Desktop for macOS](https://www.docker.com/products/docker-desktop/) page and download the installer.
2. **Install Docker Desktop**:
    - Open the downloaded `.dmg` file and drag the **Docker.app** to the Applications folder.
3. **Start Docker Desktop**:
    - Open **Docker.app** from the Applications folder.
    - Complete the setup by signing in or creating a Docker Hub account.
4. **Verify Installation**:
    - Open the Terminal and run:
        
        ```bash
        docker --version
        
        ```
        
    - The Docker version should be displayed.

---

### **3. Install Docker on Linux**

### **Supported Distributions**:

- Ubuntu
- Debian
- Fedora
- CentOS
- Other distributions may require manual installation steps.

### **Steps for Ubuntu/Debian**:

1. **Update the System**:
    
    ```bash
    sudo apt update
    sudo apt upgrade
    
    ```
    
2. **Install Dependencies**:
    
    ```bash
    sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
    
    ```
    
3. **Add Docker's Official GPG Key**:
    
    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    
    ```
    
4. **Add the Docker Repository**:
    
    ```bash
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    
    ```
    
5. **Install Docker**:
    
    ```bash
    sudo apt update
    sudo apt install -y docker-ce docker-ce-cli containerd.io
    
    ```
    
6. **Verify Installation**:
    
    ```bash
    docker --version
    
    ```
    
    - You should see the Docker version.
7. **Optional: Run Docker Without `sudo`**:
    - Add your user to the `docker` group:
        
        ```bash
        sudo usermod -aG docker $USER
        
        ```
        
    - Log out and back in for the changes to take effect.

---

### **Module: Docker Images and Containers**

### **Dockerfile**

A **Dockerfile** is a text file that contains instructions for building a Docker image. It serves as a blueprint for creating images by specifying the base image, application dependencies, configurations, and commands to run. When the Dockerfile is processed, it generates an image that can be used to create containers.

---

### **Basic Syntax of a Dockerfile**

Each line in a Dockerfile is an instruction and starts with a **Dockerfile keyword** (e.g., `FROM`, `RUN`, `CMD`). Here's a breakdown of common instructions:

| **Instruction** | **Description** |
| --- | --- |
| `FROM` | Specifies the base image (e.g., `node`, `ubuntu`). The first instruction in every Dockerfile. |
| `RUN` | Executes commands during the build process (e.g., installing dependencies). |
| `CMD` | Specifies the default command to run when the container starts. |
| `COPY` | Copies files/directories from the host machine to the image. |
| `ADD` | Similar to `COPY` but can also retrieve files from URLs. |
| `WORKDIR` | Sets the working directory inside the container. |
| `ENV` | Sets environment variables inside the container. |
| `EXPOSE` | Documents the ports the container will listen on. |
| `ENTRYPOINT` | Configures a command that will run as the container starts. |
| `VOLUME` | Declares mount points for persistent storage. |
| `LABEL` | Adds metadata to the image (e.g., version, author, description). |

---

### **Example: Basic Dockerfile**

```
# Use an official base image
FROM node:16

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code to the container
COPY . .

# Set environment variables
ENV PORT=3000

# Expose the application port
EXPOSE 3000

# Default command to run when the container starts
CMD ["npm", "start"]

```

**Explanation**:

1. Starts with the Node.js base image.
2. Sets `/app` as the working directory inside the container.
3. Copies necessary files for installing dependencies.
4. Installs dependencies with `npm install`.
5. Copies the rest of the application code.
6. Sets environment variables and exposes port 3000.
7. Defines the command to start the application (`npm start`).

---

### **Docker Images**

A **Docker image** is a lightweight, standalone, and executable package that includes everything needed to run a piece of software: the code, runtime, libraries, environment variables, configuration files, and dependencies. Images are immutable and serve as a blueprint for creating containers.

---

### **Key Features of Docker Images**

1. **Layered Architecture**:
    - Docker images are built in layers. Each layer represents a step in the Dockerfile and is cached to optimize builds.
    - Layers are shared between images to save storage space and speed up builds.
2. **Immutable**:
    - Once created, an image cannot be modified. Updates require creating a new image.
3. **Portability**:
    - Docker images can run on any machine with Docker installed, ensuring consistent environments.
4. **Versioning**:
    - Images are versioned using **tags** (e.g., `node:16`, `ubuntu:20.04`).

---

### **Common Commands for Docker Images**

### **1. Pull an Image**

Download an image from a Docker registry (e.g., Docker Hub):

```bash
docker pull ubuntu:20.04

```

### **2. List Local Images**

Show all images available on your system:

```bash
docker images

```

### **3. Build an Image**

Build an image from a `Dockerfile`:

```bash
docker build -t my-app:1.0 .

```

### **4. Tag an Image**

Add a new tag to an existing image:

```bash
docker tag my-app:1.0 my-app:latest

```

### **5. Remove an Image**

Delete an image by its ID or name:

```bash
docker rmi my-app:1.0

```

### **6. Inspect an Image**

View detailed metadata about an image:

```bash
docker inspect ubuntu:20.04

```

### **7. Push an Image**

Push an image to a registry (requires authentication):

```bash
docker push my-app:1.0

```

---

### **Creating Docker Images**

Docker images are typically created using a `Dockerfile`. Here’s an example:

### **Dockerfile Example**

```
# Base image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy application code
COPY . .

# Install dependencies
RUN pip install -r requirements.txt

# Expose application port
EXPOSE 5000

# Command to run the application
CMD ["python", "app.py"]

```

### **Build the Image**

```bash
docker build -t python-app:1.0 .

```

---

### **Docker Image Layers**

Each instruction in a Dockerfile creates a new **layer** in the image. For example:

```
FROM ubuntu:20.04       # Base layer
RUN apt-get update      # New layer for package updates
RUN apt-get install -y curl # Another layer for curl installation

```

- **Benefits of Layers**:
    - Layers are cached. If a layer hasn’t changed, Docker reuses it during builds.
    - Shared layers reduce disk space when multiple images use the same base.

---

### **Docker Image Repositories and Registries**

1. **Docker Hub**:
    - Default public registry for Docker images.
    - Examples:
        
        ```bash
        docker pull nginx:latest
        docker pull postgres:14
        
        ```
        
2. **Private Registries**:
    - Organizations can host private registries (e.g., AWS Elastic Container Registry, Google Container Registry).
3. **Local Repositories**:
    - Store and use images locally without pushing to a registry.

---

### **Viewing Docker Image Details**

### **Image History**

View the layers of an image:

```bash
docker history my-app:1.0

```

### **Image Size**

Check the size of each layer:

```bash
docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}"

```

---

### **Sharing Docker Images**

1. **Push to Docker Hub**:
    - Login:
        
        ```bash
        docker login
        
        ```
        
    - Push:
        
        ```bash
        docker push my-app:1.0
        
        ```
        
2. **Save and Load Images**:
    - Save an image to a file:
        
        ```bash
        docker save -o my-app.tar my-app:1.0
        
        ```
        
    - Load an image from a file:
        
        ```bash
        docker load -i my-app.tar
        
        ```
        

---

### **Docker Containers**

A **Docker container** is a runtime instance of a Docker image. It is lightweight, isolated, and includes everything needed to run the application or service. Containers provide a consistent environment, enabling seamless deployment across various systems.

---

### **Key Features of Docker Containers**

1. **Lightweight**:
    - Containers share the host system’s kernel, making them faster and less resource-intensive compared to virtual machines.
2. **Portable**:
    - Containers run consistently across different environments, from local development to cloud platforms.
3. **Isolated**:
    - Containers operate in isolated environments, ensuring that processes inside a container do not interfere with the host or other containers.
4. **Ephemeral**:
    - Containers can be easily created, stopped, and destroyed. Data within the container is lost unless explicitly persisted.

---

### **Lifecycle of a Docker Container**

1. **Create**:
    - A container is created from an image but not started.
    
    ```bash
    docker create nginx:latest
    
    ```
    
2. **Start**:
    - Starts a stopped or newly created container.
    
    ```bash
    docker start <container_id_or_name>
    
    ```
    
3. **Run**:
    - Creates and starts a container in one command.
    
    ```bash
    docker run nginx:latest
    
    ```
    
4. **Stop**:
    - Gracefully stops a running container.
    
    ```bash
    docker stop <container_id_or_name>
    
    ```
    
5. **Remove**:
    - Deletes a container. Ensure it is stopped before removing.
    
    ```bash
    docker rm <container_id_or_name>
    
    ```
    

---

### **Common Docker Container Commands**

### **1. Run a Container**

Run a container from an image:

```bash
docker run -d -p 8080:80 nginx

```

- `d`: Runs the container in detached mode (background).
- `p 8080:80`: Maps port 8080 on the host to port 80 inside the container.

### **2. List Containers**

View running containers:

```bash
docker ps

```

View all containers (including stopped ones):

```bash
docker ps -a

```

### **3. Access a Container’s Shell**

Enter a running container interactively:

```bash
docker exec -it <container_id_or_name> bash

```

For Alpine-based containers:

```bash
docker exec -it <container_id_or_name> sh

```

### **4. Stop a Container**

Gracefully stop a running container:

```bash
docker stop <container_id_or_name>

```

### **5. Restart a Container**

Restart a stopped or running container:

```bash
docker restart <container_id_or_name>

```

### **6. Remove a Container**

Delete a stopped container:

```bash
docker rm <container_id_or_name>

```

Force-remove a running container:

```bash
docker rm -f <container_id_or_name>

```

---

### **Inspecting Containers**

### **1. View Logs**

See logs generated by a container:

```bash
docker logs <container_id_or_name>

```

Follow the logs in real-time:

```bash
docker logs -f <container_id_or_name>

```

### **2. Inspect Container Details**

View detailed information (e.g., IP address, environment variables):

```bash
docker inspect <container_id_or_name>

```

### **3. Monitor Resource Usage**

Check CPU, memory, and network usage of containers:

```bash
docker stats

```

---

### **Persisting Data in Containers**

Containers are ephemeral, meaning data is lost when the container stops. To persist data, use **volumes** or **bind mounts**.

### **1. Using Volumes**

Volumes are managed by Docker and provide persistent storage:

```bash
docker volume create my_volume
docker run -d -v my_volume:/data nginx

```

### **2. Using Bind Mounts**

Bind mounts link a host directory to a container directory:

```bash
docker run -d -v /host/path:/container/path nginx

```

---

### **Networking in Docker Containers**

### **1. Port Mapping**

Map a container's port to the host:

```bash
docker run -d -p 8080:80 nginx

```

### **2. Docker Networks**

Docker provides different network drivers (e.g., bridge, host, overlay):

```bash
docker network create my_network
docker run --network my_network nginx

```

### **3. Connecting Containers**

Connect two containers to the same network:

```bash
docker network connect my_network container1
docker network connect my_network container2

```

---

### **Best Practices for Containers**

1. **Keep Containers Stateless**:
    - Persist data using volumes or external databases.
2. **One Process Per Container**:
    - Each container should run a single process (e.g., web server, database).
3. **Use Environment Variables**:
    - Pass configuration through environment variables:
        
        ```bash
        docker run -e ENV_VAR=value nginx
        
        ```
        
4. **Clean Up Unused Containers**:
    - Regularly remove stopped containers:
        
        ```bash
        docker container prune
        
        ```
        
5. **Monitor and Debug**:
    - Use logs and `docker stats` to monitor container performance.

---

### **Basic Docker CLI Commands**

Docker CLI provides a comprehensive set of commands to manage images, containers, networks, and volumes. Below is a categorized cheat sheet of commonly used Docker commands.

---

### **1. Docker Version and Help**

### **Check Docker Version**

Displays the installed version of Docker:

```bash
docker version

```

### **View Help for Docker Commands**

Displays usage instructions and a list of commands:

```bash
docker --help

```

Get help for a specific command:

```bash
docker <command> --help

```

---

### **2. Images**

### **Pull an Image**

Download an image from a registry (e.g., Docker Hub):

```bash
docker pull <image_name>:<tag>
# Example:
docker pull ubuntu:20.04

```

### **List Images**

View all images available locally:

```bash
docker images

```

### **Build an Image**

Build an image from a `Dockerfile`:

```bash
docker build -t <image_name>:<tag> <path_to_dockerfile>
# Example:
docker build -t my-app:1.0 .

```

### **Tag an Image**

Add a new tag to an image:

```bash
docker tag <existing_image>:<existing_tag> <new_image>:<new_tag>
# Example:
docker tag my-app:1.0 my-app:latest

```

### **Remove an Image**

Delete an image:

```bash
docker rmi <image_name>:<tag>

```

### **Save and Load Images**

Save an image to a tar file:

```bash
docker save -o <file_name>.tar <image_name>
# Example:
docker save -o my-app.tar my-app:1.0

```

Load an image from a tar file:

```bash
docker load -i <file_name>.tar

```

---

### **3. Containers**

### **Run a Container**

Create and start a container:

```bash
docker run <options> <image_name>:<tag>
# Example:
docker run -d -p 8080:80 nginx

```

**Common Options**:

- `d`: Run in detached mode (background).
- `p host_port:container_port`: Map ports between host and container.
- `-name container_name`: Assign a custom name to the container.
- `e key=value`: Set environment variables.
- `v host_path:container_path`: Mount a volume.

### **List Containers**

Show running containers:

```bash
docker ps

```

Show all containers (including stopped ones):

```bash
docker ps -a

```

### **Stop, Start, Restart Containers**

Stop a running container:

```bash
docker stop <container_id_or_name>

```

Start a stopped container:

```bash
docker start <container_id_or_name>

```

Restart a container:

```bash
docker restart <container_id_or_name>

```

### **Remove Containers**

Delete a stopped container:

```bash
docker rm <container_id_or_name>

```

Force-remove a running container:

```bash
docker rm -f <container_id_or_name>

```

Remove all stopped containers:

```bash
docker container prune

```

---

### **4. Logs and Stats**

### **View Logs**

See logs of a container:

```bash
docker logs <container_id_or_name>

```

Follow logs in real-time:

```bash
docker logs -f <container_id_or_name>

```

### **Monitor Resource Usage**

View real-time stats of running containers:

```bash
docker stats

```

---

### **5. Networks**

### **List Networks**

View all Docker networks:

```bash
docker network ls

```

### **Create a Network**

Create a custom network:

```bash
docker network create <network_name>

```

### **Connect a Container to a Network**

Attach an existing container to a network:

```bash
docker network connect <network_name> <container_name_or_id>

```

### **Disconnect a Container from a Network**

Detach a container from a network:

```bash
docker network disconnect <network_name> <container_name_or_id>

```

---

### **6. Volumes**

### **List Volumes**

Show all Docker volumes:

```bash
docker volume ls

```

### **Create a Volume**

Create a new volume:

```bash
docker volume create <volume_name>

```

### **Inspect a Volume**

View details of a specific volume:

```bash
docker volume inspect <volume_name>

```

### **Remove a Volume**

Delete a volume:

```bash
docker volume rm <volume_name>

```

Remove all unused volumes:

```bash
docker volume prune

```

---

### **7. Inspecting Resources**

### **Inspect Containers or Images**

View detailed metadata about a container or image:

```bash
docker inspect <container_id_or_image_name>

```

### **History of an Image**

View the layers that make up an image:

```bash
docker history <image_name>

```

---

### **8. Cleaning Up**

### **Remove Unused Resources**

Clean up unused containers, images, networks, and volumes:

```bash
docker system prune

```

Remove unused resources including unused images:

```bash
docker system prune -a

```

---

### **9. Export and Import Containers**

### **Export a Container**

Save a container's filesystem as a tar file:

```bash
docker export <container_id> > <file_name>.tar

```

### **Import a Container**

Create an image from an exported tar file:

```bash
docker import <file_name>.tar <image_name>:<tag>

```

---

### **10. Docker Compose**

Docker Compose is used to define and manage multi-container applications.

### **Start Services**

Start all services defined in a `docker-compose.yml` file:

```bash
docker-compose up

```

### **Stop Services**

Stop all running services:

```bash
docker-compose down

```

---

### **Module: Docker Registry and Repository**

### **DockerHub**

**DockerHub** is a cloud-based repository where Docker images are stored and shared. It serves as the default and most popular container registry, allowing developers and organizations to distribute their Dockerized applications.

---

### **Key Features of DockerHub**

1. **Image Repository**:
    - Host public and private Docker images.
    - Access official images maintained by Docker or verified publishers (e.g., `nginx`, `mysql`, `ubuntu`).
2. **Search and Explore**:
    - Search for existing images using keywords or tags.
3. **Version Control**:
    - DockerHub supports versioning through image tags (e.g., `node:14`, `node:16`).
4. **Build Automation**:
    - Automatically build images when changes are pushed to linked GitHub or Bitbucket repositories.
5. **Teams and Permissions**:
    - Collaborate on images with access control for private repositories.
6. **Integration with CI/CD**:
    - Seamlessly integrate with tools like Jenkins, GitLab, and GitHub Actions.
7. **Webhooks**:
    - Trigger actions after image push events, useful for automation.

---

### **Key Terminology**

1. **Public Repository**:
    - Accessible to everyone for free. Ideal for sharing open-source projects.
2. **Private Repository**:
    - Restricted access; requires authentication. Useful for proprietary applications.
3. **Official Images**:
    - Maintained by Docker and verified for best practices. Examples include `mysql`, `redis`, and `python`.
4. **Verified Publisher**:
    - Images from verified organizations, ensuring reliability and security.
5. **Tags**:
    - Versions or variants of an image (e.g., `node:16-alpine`).

---

### **Using DockerHub**

### **1. Creating a DockerHub Account**

- Sign up at https://hub.docker.com/.

### **2. Logging In**

Log in to DockerHub from the Docker CLI:

```bash
docker login

```

You’ll be prompted to enter your DockerHub username and password.

---

### **Pulling Images from DockerHub**

Download an image to your local system:

```bash
docker pull <image_name>:<tag>
# Example:
docker pull nginx:latest

```

### **Find Images on DockerHub**

Search for images using keywords:

```bash
docker search <keyword>
# Example:
docker search nginx

```

---

### **Pushing Images to DockerHub**

### **1. Tag Your Image**

Associate your image with a DockerHub repository:

```bash
docker tag <local_image>:<tag> <dockerhub_username>/<repository>:<tag>
# Example:
docker tag my-app:1.0 myusername/my-app:1.0

```

### **2. Push the Image**

Upload the image to DockerHub:

```bash
docker push <dockerhub_username>/<repository>:<tag>
# Example:
docker push myusername/my-app:1.0

```

---

### **Managing Repositories on DockerHub**

1. **Creating a Repository**:
    - Go to DockerHub’s website.
    - Click **Create Repository** and provide a name and description.
    - Choose public or private visibility.
2. **Viewing Repository Details**:
    - Navigate to the repository page to see tags, pull commands, and build history.
3. **Managing Access**:
    - For private repositories, grant access to specific DockerHub users.

---

### **Security and Best Practices**

1. **Use Official or Verified Images**:
    - Reduce the risk of vulnerabilities by starting with trusted sources.
2. **Scan Images**:
    - DockerHub provides automated vulnerability scanning for images.
3. **Tag Images Properly**:
    - Use meaningful tags to indicate versions or configurations (e.g., `1.0`, `latest`, `dev`).
4. **Restrict Private Repositories**:
    - Protect sensitive data by using private repositories and managing access permissions.

---

### **Example Workflow with DockerHub**

### **1. Build an Image Locally**

Create a `Dockerfile` and build an image:

```bash
docker build -t my-app:1.0 .

```

### **2. Tag the Image**

Tag the image for DockerHub:

```bash
docker tag my-app:1.0 myusername/my-app:1.0

```

### **3. Push to DockerHub**

Push the image to your DockerHub repository:

```bash
docker push myusername/my-app:1.0

```

### **4. Deploy the Image**

Pull the image from DockerHub on another machine:

```bash
docker pull myusername/my-app:1.0
docker run -d -p 8080:80 myusername/my-app:1.0

```

---