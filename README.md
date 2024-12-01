# CI/CD Pipeline for Java-based Project

This repository contains the CI/CD pipeline configuration for automating the build, test, security scan, and deployment of a Java-based project. This pipeline is designed for Jenkins and is specifically tailored for a private GitHub repository, where Git credentials and tokens are used for accessing the repository and other services.

The pipeline performs several stages including code checkout, compilation, testing, security scanning, SonarQube analysis, building Docker images, and deploying the application to Kubernetes.

**Note:** This repository only contains the pipeline configuration file (`Jenkinsfile`), not the source code of the project.

## Pipeline Overview

The pipeline automates the following stages:

1. **Git Checkout**: Clones the Git repository using stored credentials.
2. **Compile**: Runs the `mvn compile` command to compile the Java source code.
3. **Test**: Executes unit tests using `mvn test`.
4. **File System Scan**: Uses Trivy to scan the local file system for vulnerabilities.
5. **SonarQube Analysis**: Performs code quality analysis via SonarQube.
6. **Quality Gate**: Waits for SonarQube to pass the quality gate before continuing.
7. **Build**: Builds the project package using `mvn package`.
8. **Publish to Nexus**: Deploys the built package to a Nexus repository.
9. **Build & Tag Docker Image**: Builds and tags the Docker image for the application.
10. **Docker Image Scan**: Scans the Docker image for vulnerabilities using Trivy.
11. **Push Docker Image**: Pushes the Docker image to a Docker registry.
12. **Deploy to Kubernetes**: Deploys the Docker image to a Kubernetes cluster using `kubectl`.
13. **Verify the Deployment**: Verifies the deployment by checking the Kubernetes pods and services.

## Requirements

### Tools and Environment

- **JDK 17**: Used for compiling and running the Java application.
- **Maven 3**: Used for building the project and running tests.
- **SonarQube**: Used for static code analysis.
- **Trivy**: Used for security scanning of the file system and Docker images.
- **Docker**: Used to build, tag, and push Docker images.
- **Kubernetes**: Used for deploying the Docker image to a Kubernetes cluster.

### Credentials

The pipeline makes use of the following credentials, which must be configured in Jenkins:

- **git-cred**: Git credentials for accessing the private repository.
- **sonar-token**: Token used to authenticate with SonarQube.
- **docker-cred**: Docker registry credentials for pushing and pulling images.
- **k8-cred**: Kubernetes credentials for accessing and deploying to the Kubernetes cluster.

## Post-Build Actions

After the pipeline runs, the following actions are executed:

- **Email Notifications**: A detailed email is sent to notify about the build status, including a link to the console output and an attachment of the Docker image security report.
- **Status Banner**: A visual banner indicating the build status (success or failure) is included in the email.

## Conclusion

This pipeline automates the entire CI/CD workflow for a Java-based project, from building and testing to deploying and verifying on a Kubernetes cluster. Make sure to configure Jenkins with the necessary credentials and tools for this pipeline to run successfully.

For further customization or extension, you can modify the pipeline to include additional stages or change the configurations as per your requirements.

---

### Contact

For any queries or issues, feel free to contact the repository maintainers at **nishhg4@gmail.com**.
