DockerHub to AWS EC2 Deployment Workflow
![1_2NUneJQVWSVLTEjoDBNhrQ](https://github.com/Aswini-202/project2/assets/132454046/d4c64881-1215-48de-b2a2-c9e96d74bbfd)
# DockerHub to AWS EC2 Deployment Workflow

This GitHub Actions workflow automates the process of building a Docker image and deploying it to an AWS EC2 instance. It is triggered on pushes to the `master` branch of your GitHub repository.

## Workflow Overview

This workflow consists of two main jobs:

### Build Job

- This job runs on a Ubuntu runner.
- It checks out your project's code.
- Sets up Docker Buildx for multi-platform builds.
- Logs in to Docker Hub using your Docker Hub credentials.
- Builds a Docker image from your specified Dockerfile and pushes it to Docker Hub with the specified tags.

### Deploy Job

- This job also runs on a Ubuntu runner.
- It checks out your project's code.
- Logs in to Docker Hub using the Docker Hub credentials stored as environment variables.
- Sets permissions for the provided AWS private key.
- Pulls the Docker image from Docker Hub onto your AWS EC2 instance.
- Stops any running Docker container with the name 'github' on the EC2 instance.
- Removes the existing Docker container named 'github' if it exists.
- Runs a new Docker container from the pulled image with the name 'github' and forwards port 80 on the EC2 instance to port 3000 in the container.

## Prerequisites

Before using this workflow, make sure you have the following set up:

1. An AWS EC2 instance with Docker installed.
2. A Dockerfile for your project.
3. Docker Hub credentials (username and token) stored as GitHub secrets.
4. An AWS private key stored as a GitHub secret.

## Usage

1. Fork this repository.
2. Set up the required secrets in your repository's GitHub settings:
   - `DOCKER_USERNAME`: Your Docker Hub username.
   - `DOCKERHUB_TOKEN`: Your Docker Hub token.
   - `AWS_PRIVATE_KEY`: Your AWS private key.
3. Modify the paths and other configuration details in the workflow file (`./github/workflows/main.yml`) to suit your project's structure and requirements.
4. Push changes to the `master` branch of your repository to trigger the workflow.

## Security Considerations

- Ensure that AWS permissions and security groups are properly configured to allow Docker operations on your EC2 instance.
- Protect sensitive information like your AWS private key and Docker Hub token.
- Regularly rotate your AWS keys and Docker Hub tokens for security best practices.

## License

This project is licensed under the [MIT License](LICENSE).

## Acknowledgments

- Inspiration and guidance from [GitHub Actions](https://github.com/features/actions) and [Docker](https://www.docker.com/).
