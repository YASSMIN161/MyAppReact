pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build image serveur') {
            steps {
                bat 'docker build -t mern-server ./server'
            }
        }

        stage('Build image client') {
            steps {
                bat 'docker build -t mern-client ./client'
            }
        }

        stage('Docker Compose Up') {
            steps {
                bat 'docker compose down'
                bat 'docker compose up -d --build'
            }
        }

        stage('Verification') {
            steps {
                bat 'ping -n 16 127.0.0.1 > nul'
                bat 'docker ps'
                bat 'curl -f http://localhost:3000'
            }
        }
    }

    post {
        success {
            echo 'Deploiement reussi : client sur 3000, serveur sur 9000'
        }
        failure {
            bat 'docker compose logs'
            bat 'docker compose down'
        }
    }
}