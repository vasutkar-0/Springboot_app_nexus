pipeline {
    agent any

    environment {
        NEXUS_CREDENTIALS_ID = 'nexus-jenkins-creds'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/vasutkar-0/Springboot_app_nexus.git'
            }
        }

        stage('Build & Deploy to Nexus') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: "${NEXUS_CREDENTIALS_ID}",
                        usernameVariable: 'NEXUS_USER',
                        passwordVariable: 'NEXUS_PASS'
                    )
                ]) {
                    sh '''
                        mvn clean deploy -DskipTests
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment to Nexus successful'
        }
        failure {
            echo 'Build or deployment failed'
        }
    }
}
