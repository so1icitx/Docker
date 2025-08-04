# Module 2: Installation and Setup

## Overview
This module guides you through installing Docker on Windows, macOS, or Linux. You’ll set up Docker Desktop (GUI and Daemon) and verify the CLI works. By the end, you’ll have a fully functional Docker environment.

## Prerequisites
- A computer with:
  - Windows 10/11 (Pro, Enterprise, or Education) or Windows Server 2019+.
  - macOS 11.0 (Big Sur) or later.
  - A Linux distribution (e.g., Ubuntu 20.04+, CentOS 8+).
- 4GB RAM minimum (8GB recommended).
- Admin/root privileges.
- Internet connection for downloading Docker.

## Installation Instructions
Follow the platform-specific steps below, sourced from [Docker’s official documentation](https://docs.docker.com/desktop/).

### Windows
1. **Download Docker Desktop**:
   - Visit [Windows Install Guide](https://docs.docker.com/desktop/setup/install/windows-install/).
   - Download the installer (`Docker Desktop Installer.exe`).
2. **Install**:
   - Run the installer and follow the prompts.
   - Enable WSL 2 (Windows Subsystem for Linux) if prompted (recommended for better performance).
3. **Start Docker Desktop**:
   - Launch Docker Desktop from the Start menu.
   - Ensure the Docker Daemon starts (check the system tray for the Docker icon).
4. **Verify Installation**:
   ```bash
   docker version
   ```
   - Confirms CLI and Daemon versions.
   ```bash
   docker run hello-world
   ```
   - Pulls and runs a test container, verifying setup.

### macOS
1. **Download Docker Desktop**:
   - Visit [macOS Install Guide](https://docs.docker.com/desktop/setup/install/mac-install/).
   - Download the `.dmg` file for Intel or Apple Silicon.
2. **Install**:
   - Open the `.dmg` and drag Docker to the Applications folder.
   - Launch Docker Desktop from Applications.
3. **Start Docker Desktop**:
   - Ensure the Docker Daemon is running (check the menu bar).
4. **Verify Installation**:
   ```bash
   docker version
   docker run hello-world
   ```

### Linux (Ubuntu Example)
1. **Set Up Repository**:
   ```bash
   sudo apt-get update
   sudo apt-get install -y ca-certificates curl
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc
   ```
2. **Add Docker Repository**:
   ```bash
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
     $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
     sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   ```
3. **Install Docker**:
   ```bash
   sudo apt-get update
   sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```
4. **Start Docker Daemon**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```
5. **Add User to Docker Group** (to run Docker without `sudo`):
   ```bash
   sudo usermod -aG docker $USER
   newgrp docker
   ```
6. **Verify Installation**:
   ```bash
   docker version
   docker run hello-world
   ```

## Troubleshooting
- **Daemon Not Running**: Ensure Docker Desktop is open or run `sudo systemctl start docker` (Linux).
- **Permission Denied**: Add your user to the Docker group (Linux) or run as Administrator (Windows).
- **WSL 2 Issues (Windows)**: Update WSL 2 via `wsl --update` in PowerShell.

## Lab: Verify Docker Setup
1. **Check Docker Version**:
   ```bash
   docker version
   ```
   - Look for Client and Server versions to confirm the CLI and Daemon are working.
2. **Run Hello World**:
   ```bash
   docker run hello-world
   ```
   - Outputs a welcome message if Docker is set up correctly.
3. **Open Docker Desktop**:
   - Explore the GUI to see images, containers, and volumes (empty for now).

## Learning Tips
- **Use Docker Desktop**: The GUI helps visualize Docker’s state while you learn CLI commands.
- **Check System Requirements**: Ensure your OS meets Docker’s requirements to avoid installation issues.
- **Save Commands**: Document commands in a tool like Notion for quick reference.


