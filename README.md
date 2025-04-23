# Spring PetClinic GitLab CI/CD Pipeline

## Instructions

### 1. Repository Setup

Create a new empty repository in GitLab. Use GitLab instructions to add the code from your forked `spring-petclinic` repository. Add your `Dockerfile`.

---

### 2. Docker Repositories

Create **two** Docker repositories on your own **Nexus Repository** (Instruction) or on [Docker Hub](https://hub.docker.com/) called:

- `main`
- `mr`

Alternatively, you can use the **GitLab Container Registry** with **two different image names in one repository** (see Image naming convention).

---

### 3. GitLab CI/CD Pipeline Configuration

Add a `.gitlab-ci.yml` file to your repository and define the following pipeline behavior:

#### a. Merge Request Pipeline

Include the following jobs:

- **Checkstyle**  
  Use the Maven or Gradle Checkstyle plugin to generate a code style report. The report should be available as a job artifact.

- **Test**  
  Run tests using Maven or Gradle.

- **Build**  
  Build the project without running tests (using Maven or Gradle).

> **Note**: Use the `maven:3.8.5-openjdk-17` Docker image for the above three jobs.

- **Create a Docker Image**  
  Use the `Dockerfile` in the `spring-petclinic` repository to build a Docker image of the application. Tag the image using `CI_COMMIT_SHORT_SHA` and push it to the `mr` repository.

> **Note**: Refer to [Docker to build Docker images | GitLab Docs](https://docs.gitlab.com/ee/ci/docker/using_docker_build.html)

---

#### b. Main Branch Pipeline

Include the following job:

- **Create a Docker Image**  
  Build a Docker image using your `Dockerfile` and push it to the `main` repository.
