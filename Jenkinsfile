pipeline {
    agent any
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub-credentials') 
        DOCKER_HUB_USERNAME = 'tejaldb'
        IMAGE_NAME = "${DOCKER_HUB_USERNAME}/flask-app"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url:"https://github.com/tejalbhoite02/flask-application.git", branch:"main"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                }
            }
        }
        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo ${DOCKER_HUB_CREDENTIALS_PSW} | docker login -u ${DOCKER_HUB_USERNAME} --password-stdin"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}
