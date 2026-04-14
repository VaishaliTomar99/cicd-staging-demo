pipeline {
    agent any

    environment {
        IMAGE_NAME = "cicd-demo"
        CONTAINER_NAME = "cicd-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/VaishaliTomar99/cicd-staging-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:latest ."
            }
        }

        stage('Stop Old Container') {
            steps {
                sh "docker stop ${CONTAINER_NAME} || true"
                sh "docker rm ${CONTAINER_NAME} || true"
            }
        }

        stage('Run Container') {
            steps {
                sh """
                docker run -d \
                --name ${CONTAINER_NAME} \
                -p 5000:5000 \
                ${IMAGE_NAME}:latest
                """
            }
        }

        stage('Test App') {
            steps {
                sh "curl http://localhost:5000 || true"
            }
        }
    }
}
