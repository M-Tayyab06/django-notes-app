pipeline{
    
    agent {label "kali-linux"}
    stages{
        
        stage("Code"){
            steps{
                echo "This is clonning the code"
                git url: "https://github.com/M-Tayyab06/django-notes-app.git", branch:"main"
                echo "clonning is successful"
            }
        }
        stage("Build"){
            steps{
                echo "This is building the code"
                sh "whoami"
                sh 'rm -rf data/mysql/db/*'
                sh "docker compose build"
                echo "Building is successful"
            }
        }
        stage("Test"){
            steps{
                echo "This is testing the code"
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker compose up -d"
            }
        }
    }
}
