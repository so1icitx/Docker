# Module 6: Building Images

## Overview
This module teaches you how to create custom Docker images using a `Dockerfile`. You’ll build an image for a simple web application, learning how to define dependencies and configurations. Dockerfiles are the “Infrastructure as Code” (IaC) for images, enabling automation and version control.

## What is a Dockerfile?
A `Dockerfile` is a text file containing instructions to build a Docker image. It runs commands sequentially, like a shell script. Common instructions include:
- **FROM**: Specifies the base image.
- **COPY**: Adds files to the image.
- **RUN**: Executes commands during image creation.
- **EXPOSE**: Declares ports the container uses.
- **CMD**: Specifies the default command when a container starts.

## Lab: Building a Custom Image
1. **Create a Project Directory**:
   ```bash
   mkdir my-web-app
   cd my-web-app
   ```
2. **Create an HTML File**:
   - File: `index.html`
     ```html
     <!DOCTYPE html>
     <html>
     <body>
       <h1>My Docker Web App</h1>
       <p>Hello from Docker!</p>
     </body>
     </html>
     ```
3. **Create a Dockerfile**:
   - File: `Dockerfile`
     ```dockerfile
     FROM nginx:alpine
     COPY index.html /usr/share/nginx/html/index.html
     EXPOSE 80
     CMD ["nginx", "-g", "daemon off;"]
     ```
   - **Explanation**:
     - `FROM nginx:alpine`: Uses a lightweight Nginx web server image.
     - `COPY`: Adds `index.html` to the web server’s directory.
     - `EXPOSE`: Declares port 80 for HTTP.
     - `CMD`: Runs Nginx when the container starts.
4. **Build the Image**:
   ```bash
   docker build -t my-web-app:latest .
   ```
   - `-t`: Tags the image as `my-web-app:latest`.
   - `.`: Builds from the current directory.
5. **Run the Container**:
   ```bash
   docker run -d -p 8080:80 my-web-app:latest
   ```
   - Access `http://localhost:8080` to see your webpage.
6. **Verify the Image**:
   ```bash
   docker images
   ```
   - Lists `my-web-app:latest`.

## Learning Tips
- **Start Simple**: Use minimal base images like `alpine` to keep images small.
- **Layer Caching**: Docker caches each `Dockerfile` instruction; order commands to minimize rebuilds (e.g., copy static files last).
- **Test Locally**: Always test containers locally before sharing images.

## Troubleshooting
- **Build Fails**: Check `Dockerfile` syntax and ensure files (e.g., `index.html`) exist.
- **Port Not Accessible**: Verify port mapping (`-p 8080:80`) and no conflicts.
- **Image Too Large**: Use smaller base images or clean up unnecessary files.


