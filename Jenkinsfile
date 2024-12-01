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

        stage('Push to DockerHub') {
            steps {
                script {
                    try {
                        // Log into DockerHub and push the image
                        withCredentials([usernamePassword(credentialsId: 'my-docker-hub-credentials-id', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
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

