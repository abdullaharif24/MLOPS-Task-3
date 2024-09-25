pipeline {
    agent any
    
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'  // Replace with your Jenkins Docker credentials ID
        DOCKER_IMAGE = 'abdullaharif24/MlOps-Task3'  // Your Docker Hub image name
        REGISTRY_CREDENTIALS = credentials('docker-hub-credentials')  // Credentials from Jenkins
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Pull the source code from GitHub
                git branch: 'main', url: 'https://github.com/abdullaharif24/MLOPS-Task-3.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build Docker image from the Dockerfile
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using Jenkins credentials
                    sh 'echo $REGISTRY_CREDENTIALS_PSW | docker login -u $REGISTRY_CREDENTIALS_USR --password-stdin'
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }
    
    post {
        always {
            // Cleanup Docker environment
            sh 'docker logout'
            sh 'docker system prune -f'
        }
    }
}
