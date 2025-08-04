# Module 4: Volumes and Persistence

## Overview
By default, containers are ephemeral: changes to a container’s filesystem are lost when it’s deleted. This module teaches you how to use Docker volumes to persist data across container lifecycles, essential for stateful applications like databases or content management systems.

## Why Volumes?
- **Container Filesystem**: Read-write but reset to the image’s state when a new container is created.
- **Volumes**: External filesystems that persist data even if the container is deleted. Think of them as an external hard drive for your container.
- **Use Cases**: Persist database data, user uploads, or configuration files.

## Key Commands
- **docker volume create**: Creates a named volume.
- **docker volume ls**: Lists all volumes.
- **docker volume inspect**: Shows volume details (e.g., mount path).
- **docker volume rm**: Deletes a volume.
- **docker run -v**: Mounts a volume to a container.

## Lab: Using Volumes
1. **Create a Volume**:
   ```bash
   docker volume create my-data
   ```
   - Creates a named volume called `my-data`.
2. **List Volumes**:
   ```bash
   docker volume ls
   ```
   - **Output**:
     ```
     DRIVER    VOLUME NAME
     local     my-data
     ```
3. **Inspect the Volume**:
   ```bash
   docker volume inspect my-data
   ```
   - **Output** (example):
     ```
     [
         {
             "Driver": "local",
             "Name": "my-data",
             "Mountpoint": "/var/lib/docker/volumes/my-data/_data"
         }
     ]
     ```
   - Shows where the volume is stored on your host.
4. **Run a Container with a Volume**:
   ```bash
   docker run -d -p 8965:80 -v my-data:/app/data docker/getting-started:latest
   ```
   - Mounts `my-data` to `/app/data` inside the container.
5. **Verify Persistence**:
   - Stop and remove the container:
     ```bash
     docker ps
     docker stop <container_id>
     docker rm <container_id>
     ```
   - Start a new container with the same volume:
     ```bash
     docker run -d -p 8965:80 -v my-data:/app/data docker/getting-started:latest
     ```
   - Data in `/app/data` persists from the previous container.
6. **Clean Up**:
   ```bash
   docker volume ls
   docker volume rm my-data
   ```

## Learning Tips
- **Volumes vs. Containers**: Containers are temporary; volumes are permanent until deleted.
- **Mount Syntax**: `-v volume_name:container_path` links the volume to a specific path in the container.
- **Check Mountpoint**: Use `docker volume inspect` to find where data is stored on your host.

## Troubleshooting
- **Volume Not Found**: Ensure the volume was created with `docker volume create`.
- **Permission Issues**: Check host filesystem permissions if the container can’t write to the volume.
- **Data Not Persisting**: Verify the correct path is used in `-v`.


