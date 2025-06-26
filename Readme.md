# Jenkins Pipeline with Python Flask Application

This repository contains a simple Python Flask application integrated with a Jenkins Pipeline for automated build and testing.

## Project Structure

*   `app.py`: The main Flask application file.
*   `requirements.txt`: Lists the Python dependencies for the application.
*   `test_app.py`: Contains unit tests for the Flask application.
*   `jenkinsfile`: Defines the Jenkins Pipeline for CI/CD.

## Python Flask Application (`app.py`)

This is a basic Flask web application that exposes a single endpoint:

*   `/`: Returns "Hello, Jenkins Pipeline with Python!"

The application runs on `http://0.0.0.0:3001`.

### Local Setup and Run

To run the Flask application locally:

1.  **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

2.  **Run the Application**:
    ```bash
    python app.py
    ```
    The application will be accessible at `http://localhost:3001`.

## Dependencies (`requirements.txt`)

The following Python packages are required for this project:

*   `flask`: The web framework for the application.
*   `pytest`: A testing framework for Python.
*   `requests`: A library for making HTTP requests (likely used in `test_app.py`).

## Jenkins Pipeline (`jenkinsfile`)

The `jenkinsfile` defines a declarative Jenkins Pipeline with the following stages:

### `pipeline`
The root block defining the entire pipeline.

### `agent any`
Specifies that the pipeline can run on any available Jenkins agent.

### `tools`
Configures tools required by the pipeline.
*   `maven "M398"`: Installs a pre-configured Maven version named "M398" and adds it to the PATH.

### `stages`
Contains the sequential steps of the pipeline.

#### `stage('Echo Version')`
*   Prints a message "Print Maven Version".
*   Executes `mvn -version` to display the Maven version used by the pipeline.

#### `stage('Build')`
*   **(Commented out)** `git 'http://139.84.159.194:5555/dasher-org/jenkins-hello-world.git'`: This line is commented out, but would clone a Git repository if active.
*   `sh 'mvn clean package -DskipTests=true'`: Cleans the project, compiles the source code, and packages it, skipping unit tests.

#### `stage('Unit Test')`
*   `sh 'mvn test'`: Runs the unit tests defined in the project.

This pipeline automates the build and test process for a Maven-based project, ensuring that the application is correctly compiled and its tests pass.
