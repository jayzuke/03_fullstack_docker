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
                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 5'
                sh 'curl -f http://localhost:3000/items'
            }
        }
    }

    triggers {
        pollSCM('* * * * *')   // ตรวจ Git ทุก 1 นาที
    }
}
