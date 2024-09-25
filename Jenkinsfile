pipeline {
    agent any
    environment {
        // Assuming 'dockerhub-username' and 'dockerhub-password' are the IDs of the credentials
        DOCKER_USERNAME = credentials('abdullaharif24') // Loads the Docker Hub username
        DOCKER_PASSWORD = credentials('Abi112212') // Loads the Docker Hub password
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Explicitly tag and build the Docker image
                    sh "docker build -t abdullaharif24/your_dockerhub_repo:${env.BUILD_ID} ."
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    // Setup for Docker Hub credentials
                    sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                    // Pushing the Docker image/
                    sh "docker push abdullaharif24/your_dockerhub_repo:${env.BUILD_ID}"
                }
            }
        }
    }
    post {
        always {
            // Cleaning up the Docker images to save space on the Jenkins server
            echo 'Cleaning up...'
            sh "docker rmi abdullaharif24/your_dockerhub_repo:${env.BUILD_ID}"
        }
    }
}
