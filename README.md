# Tekton Pipeline Project

This project contains a Tekton pipeline configuration for automating tasks such as cloning a Git repository and building and pushing a Docker image.

## Project Structure

- `pipeline.yaml`: Defines the Tekton pipeline.
- `pipelinerun.yaml`: Contains the configuration to trigger the pipeline.
- `task.yaml`: Defines individual tasks for the pipeline.
- `Dockerfile`: Used for building the Docker image.
- `app.py`: Application source code.
- `commands/`: Directory containing additional scripts or commands.
- `requirements.txt`: Python dependencies for the project.

## Pipeline Overview

The pipeline consists of the following tasks:

1. **Fetch Repository**:
   - Clones the specified Git repository.
   - Parameters:
     - `url`: URL of the Git repository.
     - `deleteExisting`: Whether to clean the workspace before cloning.

2. **Build**:
   - Builds and pushes a Docker image using Buildah.
   - Parameters:
     - `IMAGE`: Name of the Docker image.
     - `IMAGE_PUSH_SECRET_NAME`: Secret for DockerHub authentication.

## Usage

1. Replace placeholders in `pipeline.yaml`:
   - `{YOUR_GIT_REPOSITORY_URL}`: Replace with your Git repository URL.
   - `{YOUR_DOCKERHUB_REPOSITORY_NAME}`: Replace with your DockerHub repository name.

2. Apply the pipeline configuration:
   ```bash
   kubectl apply -f pipeline.yaml
   ```

3. Trigger the pipeline using `pipelinerun.yaml`:
   ```bash
   kubectl apply -f pipelinerun.yaml
   ```

4. Monitor the pipeline execution:
   ```bash
   tkn pipeline logs -f tutorial-pipeline
   ```

## Prerequisites

- Tekton Pipelines installed on your Kubernetes cluster.
- DockerHub account for pushing images.
- Kubernetes secret for DockerHub authentication (`image-push-secrets`).

## License

This project is licensed under the MIT License.