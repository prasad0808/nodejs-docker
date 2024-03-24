pipeline {
    agent any
    environment {
        // Define the ECR repository URL
        ECR_REPOSITORY_URL = '377116394631.dkr.ecr.us-east-1.amazonaws.com/nodejs-docker'
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Login to ECR
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ECR_REPOSITORY_URL}'

                    // Build the Docker image
                    sh 'docker build -t ${ECR_REPOSITORY_URL}:latest .'
                }
            }
        }
        stage('Push to AWS ECR') {
            steps {
                script {
                    // Push the image to ECR
                    sh 'docker push ${ECR_REPOSITORY_URL}:latest'
                }
            }
        }
    }
}