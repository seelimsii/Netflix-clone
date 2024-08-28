pipeline {
    agent any

    environment {
        DOCKER_IMAGE_CONTROL_PANEL = 'control-panel:latest'
        DOCKER_IMAGE_NETFLIX_CLONE = 'netflix-clone:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/seelimsii/Netflix-clone'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE_CONTROL_PANEL}", "-f control-pannel/Dockerfile ./control-pannel")
                    docker.build("${DOCKER_IMAGE_NETFLIX_CLONE}", "-f Netflix-clone/Dockerfile ./Netflix-clone")
                }
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
