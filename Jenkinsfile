pipeline {
    agent any

    environment {
        GIT_REPOSITORY_URL = 'https://github.com/purvagiri2001/jenkins-all-.git'
        DOCKER_IMAGE_NAME = 'purvagiri2001/docker_jenkins_demo'
        IMAGE_TAG = '1.0'
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    try {
                        // Cloning the repository
                        git branch: 'main', url: GIT_REPOSITORY_URL
                    } catch (Exception e) {
                        // If cloning fails, print the error message
                        echo "Failed to clone repository: ${e.message}"
                        error "Failed to clone repository"
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    try {
                        // Build and tag the Docker image
                        echo "Building Docker image: ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}"
                        sh "docker build -t ${DOCKER_IMAGE_NAME}:${IMAGE_TAG} ."
                    } catch (Exception e) {
                        // If the build fails, print the error message
                        echo "Failed to build Docker image: ${e.message}"
                        error "Failed to build Docker image"
                    }
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    try {
                        // Log into DockerHub and push the image
                        withCredentials([usernamePassword(credentialsId: 'test', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                            // Explicit login before push
                            sh """
                                echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                                docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}
                            """
                        }
                    } catch (Exception e) {
                        // If the push fails, print the error message
                        echo "Failed to push Docker image to registry: ${e.message}"
                        error "Failed to push Docker image"
                    }
                }
            }
        }
    }
}
