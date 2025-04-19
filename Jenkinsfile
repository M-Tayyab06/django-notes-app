@Library('Shared') _
pipeline {
    
    agent { label "kali-linux" }

    stages {
        stage('Hello'){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code Cloning") {
            steps {
                script{
                    clone("https://github.com/M-Tayyab06/django-notes-app.git","main")
                }
            }
        }

        stage("Build") {
            steps {
                script{
                    docker_build("notes-app","latest","mtayyab06")
                }
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script{
                    docker_push("notes-app","latest","mtayyab06")
                }
            }
        }
        stage("Deploy") {
            steps {
                script{
                    docker_compose()
                }
            }
        }
    }
}
