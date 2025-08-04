# Module 3: Basic Docker Commands

## Overview
This module covers essential Docker CLI commands to pull images, run containers, and manage them. You’ll learn how to start, stop, and inspect containers using the `docker/getting-started` image as an example.

## Key Commands
- **docker pull**: Downloads an image from a registry (e.g., Docker Hub).
- **docker images**: Lists local images.
- **docker run**: Creates and starts a container from an image.
- **docker ps**: Shows running containers.
- **docker stop/kill**: Stops a container gracefully (`stop`) or forcefully (`kill`).
- **docker rm**: Removes a stopped container.

## Lab: Running Your First Container
1. **Pull an Image**:
   ```bash
   docker pull docker/getting-started:latest
   ```
   - Downloads the `docker/getting-started` image from Docker Hub.
   - **Output**: Shows layers being pulled (e.g., `latest: Pulling from docker/getting-started`).
2. **List Images**:
   ```bash
   docker images
   ```
   - **Output**:
     ```
     REPOSITORY           TAG       IMAGE ID       CREATED       SIZE
     docker/getting-started   latest    a1b2c3d4e5f6   1 month ago   123MB
     ```
3. **Run a Container**:
   ```bash
   docker run -d -p 8965:80 docker/getting-started:latest
   ```
   - **Flags**:
     - `-d`: Runs in detached mode (background).
     - `-p 8965:80`: Maps port 8965 (host) to port 80 (container, HTTP).
     - `docker/getting-started:latest`: Specifies the image and tag.
   - **Output**: A container ID (e.g., `1a2b3c4d5e6f`).
4. **Check Running Containers**:
   ```bash
   docker ps
   ```
   - **Output**:
     ```
     CONTAINER ID   IMAGE                     COMMAND                  CREATED        STATUS        PORTS                    NAMES
     1a2b3c4d5e6f   docker/getting-started:latest   "/docker-entrypoint.…"   10 seconds ago Up 10 seconds 0.0.0.0:8965->80/tcp   random-name
     ```
   - **Explanation**: Shows the container ID, image, ports (`0.0.0.0:8965->80/tcp`), and status.
5. **Access the Container**:
   - Open a browser and navigate to `http://localhost:8965`.
   - **Result**: Displays a webpage served by the container.
6. **Stop the Container**:
   ```bash
   docker stop 1a2b3c4d5e6f
   ```
   - Sends a `SIGTERM` signal to gracefully stop the container.
   - Verify with `docker ps` (should be empty).
7. **Remove the Container**:
   ```bash
   docker ps -a
   ```
   - Lists all containers, including stopped ones.
   ```bash
   docker rm 1a2b3c4d5e6f
   ```
   - Deletes the stopped container.

## Learning Tips
- **Understand Port Mapping**: `-p hostport:containerport` connects your machine’s port to the container’s (e.g., `8965:80` for HTTP).
- **Use `docker ps -a`**: Always check stopped containers before removing them.
- **Avoid `docker kill`**: Use `stop` unless the container is unresponsive, as `kill` (SIGKILL) is forceful.

## Troubleshooting
- **Port Conflict**: If port 8965 is in use, try another (e.g., `-p 8080:80`).
- **Image Not Found**: Ensure `docker pull` completed successfully.
- **Container Exited**: Check logs with `docker logs <container_id>` for errors.


