pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ape-aakrit/final.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh "docker compose -f ${COMPOSE_FILE} build"
            }
        }

        stage('Deploy Containers') {
            steps {
                sh "docker compose -f ${COMPOSE_FILE} down"
                sh "docker compose -f ${COMPOSE_FILE} up -d"
            }
        }
    }

    post {
        always {
            sh 'docker ps -a'
        }
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed. Check console output.'
        }
    }
}
