pipeline {
    agent any
    environment {
        // Assuming 'dockerhub-username' and 'dockerhub-password' are the IDs of the credentials
        DOCKER_USERNAME = credentials('dockerhub-username') // Loads the Docker Hub username
        DOCKER_PASSWORD = credentials('dockerhub-password') // Loads the Docker Hub password
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Explicitly tag and build the Docker image
                    sh "docker build -t abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID} ."
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    // Setup for Docker Hub credentials
                    sh 'echo $DOCKER_PASSWORD | docker login --username $DOCKER_USERNAME --password-stdin'
                    // Pushing the Docker image/
                    sh "docker push abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}"
                }
            }
        }
    }
    post {
        always {
            // Cleaning up the Docker images to save space on the Jenkins server
            echo 'Cleaning up...'
            sh "docker rmi abdullahdaniyal1234/your_dockerhub_repo:${env.BUILD_ID}"
        }
    }
}
