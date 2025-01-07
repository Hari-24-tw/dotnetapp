# GitHub Actions Workflow for .NET Application

This repository contains a GitHub Actions workflow for building, analyzing, and deploying a .NET application. The workflow is defined in the `dotnet-pipeline.yaml` file.

## Workflow: `dotnet-pipeline.yaml`

### Description
This workflow is triggered on push events to the `main` branch and can also be triggered manually using the `workflow_dispatch` event. It builds the .NET application, runs SonarQube analysis, and deploys the application to different environments.

### Features

- **Trigger Events**:
  - `push` to `main` branch
  - `workflow_dispatch`

- **Environment Variables**:
  - `SONARQUBE_TOKEN`: SonarQube token for authentication.

- **Job: build**:
  - **Runs-on**: `ubuntu-22.04`
  - **Steps**:
    - **Checkout repository**: Uses `actions/checkout@v4` to check out the repository code.
    - **Setup .NET**: Uses `actions/setup-dotnet@v4` to set up .NET version `8.0.x`.
    - **Restore dependencies**: Runs `dotnet restore` to restore the project's dependencies.
    - **Run SonarQube Scanner**: Installs and runs the SonarQube scanner for code analysis.
    - **Build .NET application**: Runs `dotnet build` to build the application in Release configuration.
    - **Upload build artifact**: Uses `actions/upload-artifact@v4.5.0` to upload the build artifact.

- **Job: deploy-dev**:
  - **Runs-on**: `ubuntu-22.04`
  - **Environment**: `Dev`
  - **Needs**: `build` job
  - **Steps**:
    - **Deployment to Dev Environment**: Placeholder command to simulate deployment to the Dev environment.

- **Job: deploy-prod**:
  - **Runs-on**: `ubuntu-22.04`
  - **Environment**: `Prod`
  - **Needs**: `deploy-dev` job
  - **Steps**:
    - **Deployment to Prod Environment**: Placeholder command to simulate deployment to the Prod environment.

- **Job: docker-build**:
  - **Runs-on**: `ubuntu-22.04`
  - **Steps**:
    - **Build Docker Image**: Builds a Docker image for the application and lists the Docker images.

### Pipeline Execution Steps
1. Push code to the `main` branch or trigger the workflow manually from the GitHub Actions tab.
2. The `build` job starts and runs the build steps.
3. The build artifact is uploaded.
4. The `deploy-dev` job starts after the `build` job completes.
5. The `deploy-prod` job starts after the `deploy-dev` job completes.
6. The `docker-build` job builds a Docker image for the application.

## Conclusion
This workflow provides a CI/CD pipeline for building, analyzing, and deploying a .NET application to multiple environments. It includes steps for code analysis using SonarQube and building a Docker image for the application.