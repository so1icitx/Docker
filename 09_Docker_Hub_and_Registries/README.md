# Module 9: Docker Hub and Registries

## Overview
This module covers Docker Hub and alternative registries for storing and sharing Docker images. You’ll learn how to push and pull images, manage repositories, and explore other registry options.

## What is Docker Hub?
Docker Hub is the official cloud service for storing and sharing Docker images. It hosts public and private repositories, offering pre-built images like `nginx`, `python`, and `docker/getting-started`.

- **Alternatives**:
  - AWS Elastic Container Registry (ECR)
  - Google Cloud Artifact Registry
  - Azure Container Registry
- **Choosing a Registry**: Use Docker Hub for public images or learning; use cloud registries for private, enterprise deployments.

## Lab: Using Docker Hub
1. **Create a Docker Hub Account**:
   - Sign up at [Docker Hub](https://hub.docker.com/).
2. **Log In via CLI**:
   ```bash
   docker login
   ```
   - Enter your Docker Hub username and password.
3. **Tag Your Image**:
   ```bash
   docker tag my-web-app:latest <your_username>/my-web-app:latest
   ```
   - Replaces `<your_username>` with your Docker Hub username.
4. **Push the Image**:
   ```bash
   docker push <your_username>/my-web-app:latest
   ```
   - Uploads your image to Docker Hub.
5. **Pull and Test**:
   - Remove the local image:
     ```bash
     docker rmi <your_username>/my-web-app:latest
     ```
   - Pull it back:
     ```bash
     docker pull <your_username>/my-web-app:latest
     ```
   - Run it:
     ```bash
     docker run -d -p 8080:80 <your_username>/my-web-app:latest
     ```
   - Verify at `http://localhost:8080`.
6. **Explore Alternative Registries**:
   - Visit [AWS ECR](https://aws.amazon.com/ecr/), [Google Artifact Registry](https://cloud.google.com/artifact-registry), or [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) to understand their features.

## Learning Tips
- **Public vs. Private**: Public repositories are free on Docker Hub; private ones require a paid plan.
- **Tagging**: Always specify tags (e.g., `latest`, `v1.0`) to track versions.
- **Registry Choice**: Use cloud registries for production to integrate with your cloud provider.

## Troubleshooting
- **Login Failed**: Verify your Docker Hub credentials and internet connection.
- **Push Denied**: Ensure you’re logged in and the repository exists.
- **Rate Limits**: Docker Hub has pull limits for free accounts; consider paid plans for heavy use.

## Next Steps
You’ve completed the course! Review the modules, experiment with new images, and explore [Docker’s documentation](https://docs.docker.com/) for advanced topics like Docker Compose or multi-container apps.
