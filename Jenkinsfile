pipeline {
    agent any

    environment {
        // Define environment variables for Docker Hub credentials
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub')
        DOCKER_IMAGE_NAME = 'rajatherise/phpnew'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the Git repository
                checkout scm
            }
        }

        stage('Build and Push to Docker Hub') {
            steps {
                // Build and tag the Docker image
                script {
                    def dockerImage = docker.build(env.DOCKER_IMAGE_NAME)
                }

                // Log in to Docker Hub
                script {
                    withDockerRegistry([credentialsId: env.DOCKER_HUB_CREDENTIALS]) {
                        // Push the Docker image to Docker Hub
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded! The Docker image has been built and pushed to Docker Hub.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
