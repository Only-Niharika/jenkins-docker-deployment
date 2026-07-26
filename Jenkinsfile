pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Only-Niharika/jenkins-docker-deployment.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-docker-app .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh 'docker stop jenkins-docker-container || true'
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm jenkins-docker-container || true'
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 80:80 --name jenkins-docker-container jenkins-docker-app'
            }
        }
    }
}
