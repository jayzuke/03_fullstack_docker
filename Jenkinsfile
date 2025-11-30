pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh '''
                    docker compose build
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker compose down
                    docker compose up -d
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh '''
                    sleep 5
                    curl -f http://localhost:8080 || exit 1
                '''
            }
        }
    }
}
