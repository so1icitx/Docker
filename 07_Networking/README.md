# Module 7: Docker Networking

## Overview
This module covers Docker’s networking capabilities, including exposing containers to the host, communicating between containers, and running containers in offline mode. You’ll learn how to configure networking for security and efficiency, with a focus on the `--network none` flag for isolation.

## Docker Networking Basics
Docker containers use networks to communicate with the host, other containers, or the internet. Docker provides several network modes:
- **bridge**: Default mode; containers on the same host can communicate via a virtual network.
- **host**: Container uses the host’s network stack (no isolation).
- **none**: Disables all networking, isolating the container from external connections.

**Analogy**: Think of Docker networking as a phone system. The `bridge` network is like an internal office network, `host` is like using the company’s main line, and `none` is like unplugging the phone entirely.

## Why Offline Mode?
The `--network none` flag disables all network access, useful for:
- Running untrusted third-party code.
- Creating secure environments (e.g., for e-learning platforms executing student code).
- Isolating containers with potential security risks to prevent malicious network activity.

## Key Commands
- **docker run --network**: Specifies the network mode (e.g., `none`, `bridge`).
- **docker network ls**: Lists available networks.
- **docker network inspect**: Shows network details.
- **docker run -p**: Maps host ports to container ports.

## Lab: Configuring Networking
1. **Run a Container with Default Networking**:
   ```bash
   docker run -d -p 8965:80 docker/getting-started:latest
   ```
   - Maps port 8965 (host) to 80 (container).
   - Access `http://localhost:8965` to verify.
2. **Check Running Containers**:
   ```bash
   docker ps
   ```
   - **Output**:
     ```
     CONTAINER ID   IMAGE                     PORTS                    NAMES
     1a2b3c4d5e6f   docker/getting-started:latest   0.0.0.0:8965->80/tcp   random-name
     ```
3. **Run a Container in Offline Mode**:
   ```bash
   docker run -d --network none docker/getting-started:latest
   ```
   - Note the container ID.
   - Try accessing `http://localhost:8965` (should fail due to no network).
4. **Inspect the Network**:
   ```bash
   docker network ls
   ```
   - **Output**:
     ```
     NETWORK ID     NAME      DRIVER    SCOPE
     abc123def456   bridge    bridge    local
     def456abc123   host      host      local
     ghi789jkl012   none      none      local
     ```
   - The container uses the `none` network, isolating it.
5. **Verify Isolation**:
   ```bash
   docker exec <container_id> ping google.com
   ```
   - **Output**: Fails with `ping: google.com: Name or service not known`.
6. **Clean Up**:
   ```bash
   docker stop <container_id>
   docker rm <container_id>
   ```

## Learning Tips
- **Understand Network Modes**: `bridge` for most apps, `none` for isolation, `host` for performance.
- **Test Connectivity**: Use `ping` or `curl` inside containers to verify network behavior.
- **Port Mapping**: Always specify `-p` for services needing external access (e.g., web servers).

## Troubleshooting
- **No Network Access**: Confirm the correct network mode (`docker inspect <container_id>`).
- **Port Conflicts**: Ensure the host port (e.g., 8965) isn’t used by another process.
- **Offline Mode Issues**: Verify `--network none` is set correctly if isolation is intended.

