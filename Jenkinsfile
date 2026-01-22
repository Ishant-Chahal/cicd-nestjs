pipelime {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "ishantchahal39@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps{
                git branch: 'main', url: 'https://github.com/Ishant-Chahal/cicd-nestjs.git'
            }
        }

        stage('Build Docker Image'){
            steps{
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & Remove Previous Container'){
            steps{
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker Container Run'){
            steps{
                sh '''
                    docker run -d -p ${PORT}:{PORT} --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

        stage('Send Email Notification'){
            steps{
                emailext{
                    subject: "Nestjs app deployed",
                    body: "Your Nestjs app is deloyed on http://13.51.204.190:${PORT}/",
                    to: "${EMAIL}"
                }
            }
        }
    }
}