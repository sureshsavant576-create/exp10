
pipeline {
    agent any

    stages {
        stage('Docker Verification') {
            steps {
                echo 'Checking Docker installation...'

                bat 'where docker'
                bat 'docker --version'
                bat 'docker info'
                bat 'docker ps'
            }
        }
    }
}
