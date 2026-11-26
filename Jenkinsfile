
pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"

        DOCKER = "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe"

        PYTHON = "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\Python\\Python313\\python.exe"
    }

    stages {

        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                echo "Checking Python installation..."

                bat "\"${PYTHON}\" --version"

                echo "Verifying Python syntax..."

                bat "\"${PYTHON}\" -m py_compile app.py"

                echo "Python syntax verification successful!"
            }
        }

        stage('3. Docker Verification') {
            steps {
                bat "\"${DOCKER}\" --version"
                bat "\"${DOCKER}\" ps"
            }
        }

        stage('4. Build & Tag Docker Image') {
            steps {
                bat "\"${DOCKER}\" build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} -t ${REGISTRY}/${IMAGE_NAME}:latest ."
            }
        }

        stage('5. Push Image to Registry') {
            steps {
                bat "\"${DOCKER}\" push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"

                bat "\"${DOCKER}\" push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "SUCCESS! Docker image pushed to local registry."
        }

        failure {
            echo "Pipeline failed. Check the console output."
        }
    }
}
