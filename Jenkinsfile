pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/saiteja-adapa-2909/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("flask-docker-app:${env.BUILD_ID}")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    docker.image("flask-docker-app:${env.BUILD_ID}").run("-d -p 5000:5000 --name flask-app-${env.BUILD_ID}")
                }
            }
        }

        stage('Clean Up') {
            steps {
                script {
                    sh 'docker stop flask-app-${env.BUILD_ID}'
                    sh 'docker rm flask-app-${env.BUILD_ID}'
                }
            }
        }
    }
}