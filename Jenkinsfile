pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "sample-java"
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Code already checked out from SCM"
            }
        }

        stage('Build & Deploy using Docker Compose') {
            steps {
                sh '''
                  docker compose down || true
                  docker compose up -d --build
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment Successful 🚀"
        }
        failure {
            echo "Deployment Failed ❌"
        }
    }
}
