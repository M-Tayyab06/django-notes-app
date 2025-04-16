pipeline {
    agent { label "kali-linux" }

    environment {
        IMAGE_NAME = "django_app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage("Code") {
            steps {
                echo "Cloning the code..."
                git url: "https://github.com/M-Tayyab06/django-notes-app.git", branch: "main"
                echo "Cloning successful!"
            }
        }

        stage("Build") {
            steps {
                echo "Building Docker image..."
                sh "whoami"
                sh "docker-compose down -v || true"
                sh "docker-compose build"
                sh "docker images"
                echo "Build successful!"
            }
        }

        stage("Push") {
            steps {
                echo "Pushing Docker image to Docker Hub..."
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCred',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD')]) {

                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'

                    sh """
                        docker image tag ${IMAGE_NAME}:${IMAGE_TAG} $DOCKER_USERNAME/${IMAGE_NAME}:${IMAGE_TAG}
                        docker push $DOCKER_USERNAME/${IMAGE_NAME}:${IMAGE_TAG}
                    """
                }
                echo "Image pushed to Docker Hub!"
            }
        }

        stage("Test") {
            steps {
                echo "Testing the application (manual or automated test step can go here)..."
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the Docker container..."
                sh "docker-compose up -d"
                sh "docker ps"
                echo "Deployment completed!"
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed!"
        }
        success {
            echo "Pipeline completed successfully!"
        }
    }
}
