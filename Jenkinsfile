pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    environment {
        ECR_REPO_NAME = "underwater"  // Buradaki adı image adıyla aynı olarak ayarlayabilirsiniz
        AWS_REGION = "eu-central-1"
        AWS_CREDENTIALS = "aws-credentials"
    }
    stages {
        stage('Clone repository') {
            steps {
                script {
                    checkout scm
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    app = docker.build(ECR_REPO_NAME)
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Empty'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry("https://059797956936.dkr.ecr.eu-central-1.amazonaws.com","ecr:eu-central-1:${AWS_CREDENTIALS}") {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }
}
