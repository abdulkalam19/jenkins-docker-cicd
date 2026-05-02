pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t abdulkalam-webapp .'
            }
        }
        stage('Stop Old Container') {
            steps {
                echo 'Stopping old container if running...'
                bat 'docker stop webapp || exit 0'
                bat 'docker rm webapp || exit 0'
            }
        }
        stage('Deploy Container') {
            steps {
                echo 'Deploying new container...'
                bat 'docker run -d --name webapp -p 8081:80 abdulkalam-webapp'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! App running at http://localhost:8081'
        }
        failure {
            echo 'Pipeline failed. Check the logs above.'
        }
    }
}
