# Module 5: Interacting with Containers

## Overview
This module teaches you how to execute commands, access shells, and view logs inside running containers. You’ll learn to troubleshoot and inspect containers using `docker exec` and `docker logs`, essential for debugging or managing applications.

## Key Commands
- **docker exec**: Runs a command inside a running container.
- **docker exec -it**: Starts an interactive shell session (`-i` for interactive, `-t` for a tty).
- **docker logs**: Views a container’s logs for debugging.

## Lab: Interacting with a Container
1. **Start a Container**:
   ```bash
   docker run -d -p 8965:80 docker/getting-started:latest
   ```
   - Note the container ID from `docker ps`.
2. **Run a One-Off Command**:
   ```bash
   docker exec <container_id> ls /app
   ```
   - Lists files in the `/app` directory inside the container.
   - **Output** (example):
     ```
     data  index.html
     ```
3. **Start an Interactive Shell**:
   ```bash
   docker exec -it <container_id> /bin/sh
   ```
   - Opens a shell inside the container.
   - Try commands like:
     ```bash
     whoami
     cat /etc/os-release
     ```
   - Exit the shell with `exit`.
4. **View Logs**:
   ```bash
   docker logs <container_id>
   ```
   - Shows the container’s output (e.g., web server logs).
   - **Output** (example):
     ```
     2025/08/01 10:15:01 [notice] 1#1: start worker processes
     192.168.1.100 - - [01/Aug/2025:10:15:02 +0000] "GET / HTTP/1.1" 200 612
     ```
5. **Clean Up**:
   ```bash
   docker stop <container_id>
   docker rm <container_id>
   ```

## Learning Tips
- **Interactive Shells**: Use `/bin/sh` or `/bin/bash` depending on the container’s OS (check with `docker inspect <container_id>`).
- **Logs for Debugging**: Always check `docker logs` when a container fails to start.
- **Detached vs. Interactive**: Use `-d` for background tasks, `-it` for interactive sessions.

## Troubleshooting
- **No Shell Available**: Some containers (e.g., minimal images) may lack `/bin/sh`. Use `docker inspect` to check available commands.
- **Container Not Running**: Ensure the container is active with `docker ps`.
- **Permission Denied**: Verify you have access to the container’s filesystem.

