# Module 8: Resource Management

## Overview
This module teaches you how to monitor and limit container resources using `docker stats`, `docker top`, and resource-limiting flags. You’ll learn to track CPU and memory usage and prevent containers from overloading your system.

## Why Resource Management?
Containers can consume significant resources (CPU, memory), slowing down your host machine. Monitoring and limiting resources ensures efficient performance, especially in production environments.

- **Use Cases**:
  - Identify resource-hogging containers.
  - Limit resources for untrusted or resource-intensive applications.
  - Optimize server performance in multi-container setups.

## Key Commands
- **docker stats**: Displays live resource usage (CPU, memory) for running containers.
- **docker top**: Shows running processes inside a container.
- **docker run --memory**: Limits the container’s memory usage.
- **docker run --cpus**: Limits the container’s CPU shares.

## Lab: Monitoring and Limiting Resources
1. **Start a Container**:
   ```bash
   docker run -d -p 8965:80 docker/getting-started:latest
   ```
   - Note the container ID.
2. **Monitor Resource Usage**:
   ```bash
   docker stats
   ```
   - **Output** (example):
     ```
     CONTAINER ID   NAME         CPU %     MEM USAGE / LIMIT   MEM %     NET I/O
     1a2b3c4d5e6f   random-name  0.10%     25MiB / 8GiB       0.31%     1.2kB / 0B
     ```
   - Shows CPU, memory, and network usage.
3. **View Processes**:
   ```bash
   docker top <container_id>
   ```
   - **Output** (example):
     ```
     PID   USER   COMMAND
     1234  root   nginx: master process
     5678  nginx  nginx: worker process
     ```
   - Lists processes running inside the container.
4. **Limit Resources**:
   - Stop and remove the container:
     ```bash
     docker stop <container_id>
     docker rm <container_id>
     ```
   - Run with resource limits:
     ```bash
     docker run -d -p 8965:80 --memory="256m" --cpus="0.5" docker/getting-started:latest
     ```
     - `--memory="256m"`: Limits memory to 256MB.
     - `--cpus="0.5"`: Limits CPU to 0.5 cores.
5. **Verify Limits**:
   ```bash
   docker inspect <container_id> | grep -i memory
   ```
   - Confirms memory limit (e.g., `"Memory": 268435456`).
   ```bash
   docker inspect <container_id> | grep -i cpu
   ```
   - Confirms CPU limit (e.g., `"NanoCpus": 500000000`).
6. **Clean Up**:
   ```bash
   docker stop <container_id>
   docker rm <container_id>
   ```

## Learning Tips
- **Use `stats` Regularly**: Monitor resource usage to catch runaway containers.
- **Combine `stats` and `top`**: Use `stats` for container-level usage, `top` for process-level details.
- **Set Conservative Limits**: Start with low memory (`--memory="128m"`) and CPU (`--cpus="0.25"`) for testing.

## Troubleshooting
- **High Resource Usage**: Check `docker stats` and limit with `--memory` or `--cpus`.
- **Container Crashes**: Use `docker logs` to diagnose resource-related issues.
- **Limits Not Applied**: Verify flags with `docker inspect`.


