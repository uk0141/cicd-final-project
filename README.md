# cicd-final-project

## CI/CD Tools and Practices Final Project

This project demonstrates Continuous Integration and Continuous Delivery (CI/CD) using GitHub Actions, Tekton Pipelines, Buildah, and OpenShift.

The project automates code quality checks, unit testing, container image building, and application deployment.

## Project Objectives

- Automate code linting using Flake8.
- Run automated unit tests using Nose.
- Configure GitHub Actions for continuous integration.
- Define Tekton tasks for cleaning the source workspace and running tests.
- Build a container image using Buildah.
- Deploy the application to OpenShift.
- Verify that the deployed application runs successfully.

## Technologies Used

- Python 3.9
- Flask
- Flake8
- Nose
- Git and GitHub
- GitHub Actions
- Tekton Pipelines
- Buildah
- OpenShift
- Docker-compatible container images

## Repository Structure

```text
ci-cd-final-project/
├── .github/
│   └── workflows/
│       └── workflow.yml
├── .tekton/
│   └── tasks.yml
├── bin/
├── service/
├── tests/
├── Dockerfile
├── Procfile
├── requirements.txt
├── setup.cfg
├── README.md
└── LICENSE
```

## Prerequisites

Before running the project, ensure that you have:

- Python and pip installed.
- Git installed.
- Access to GitHub Actions.
- Access to the course OpenShift environment for pipeline execution and deployment.
- The required project dependencies listed in `requirements.txt`.

## Installation

Clone the repository:

```bash
git clone https://github.com/uk0141/ci-cd-final-project.git
cd ci-cd-final-project
```

Install the project dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If you are using the course lab environment, run its setup script when required:

```bash
bash bin/setup.sh
```

If the setup script asks you to restart the terminal, exit the shell and open a new one.

## Code Quality Checks

The project uses Flake8 to identify Python coding-style problems.

Run the linting checks with:

```bash
flake8 service tests --count --show-source --statistics
```

The linting step is configured in the GitHub Actions workflow at:

`.github/workflows/workflow.yml`

## Unit Testing

The project uses Nose to execute automated unit tests.

Run the tests with:

```bash
nosetests
```

Nose coverage settings are configured in `setup.cfg`.

The GitHub Actions workflow installs the dependencies, runs Flake8, and executes the Nose tests whenever a push or pull request targets the `main` branch.

## GitHub Actions Continuous Integration

The CI workflow is located at:

`.github/workflows/workflow.yml`

The workflow performs the following steps:

1. Checks out the repository.
2. Sets up Python.
3. Installs the dependencies.
4. Runs Flake8 linting.
5. Runs Nose unit tests.

To review workflow execution results, open the repository's **Actions** tab on GitHub.

A successful run should show that all configured steps have completed without errors.

## Tekton Tasks

The Tekton task definitions are stored in:

`.tekton/tasks.yml`

The cleanup task removes existing files from the configured source workspace before subsequent processing. The test task installs dependencies, runs Flake8, and executes Nose unit tests.

The Tekton pipeline must provide the correct source workspace path and configure the tasks in the intended execution order.

## OpenShift Pipeline

The course pipeline uses the following stages:

1. `cleanup`
2. `git-clone`
3. `flake8` or ESLint
4. `nose` or Jest
5. `buildah`
6. `deploy` using the appropriate OpenShift deployment task

The pipeline checks out the source code, performs quality and test checks, builds a container image, and deploys the application.

The actual pipeline configuration and successful execution must be verified in the OpenShift course environment.

## Application Verification

After deployment, inspect the application logs in OpenShift and verify that the application starts successfully.

For this project, the expected application log should include the `SERVICERUNNING` message and indicate that the application is listening on port `8000`.

Example of the expected log format:

```text
[INFO] Starting gunicorn 20.1.0
[INFO] Listening at: http://0.0.0.0:8000
[INFO] SERVICERUNNING
[INFO] Using worker: sync
```

These lines illustrate the expected format; confirm the actual messages in your deployed application's logs.

## Troubleshooting

### Dependency installation fails

Confirm that Python and pip are available, then retry:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Flake8 reports errors

Review the reported filenames and line numbers, correct the code issues, and run Flake8 again.

### Nose tests fail

Check the test output, verify that dependencies are installed, and confirm that the test files and application code are present.

### GitHub Actions fails

Open the **Actions** tab, select the failed workflow run, and inspect the failing step's logs.

### OpenShift deployment fails

Review the pipeline task logs, image-build output, deployment status, and application logs in the course OpenShift environment.

## License

This project uses the Apache License. See the [LICENSE](LICENSE) file for details.

## Author

Created as part of the CI/CD Tools and Practices final project.
