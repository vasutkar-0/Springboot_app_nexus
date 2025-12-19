pipeline {
    agent any
    tools {
        maven 'Maven-3.9.12'
    }

    environment {
        NEXUS_CREDENTIALS_ID = 'nexus-jenkins-creds'
    }

    stages {

        stage('Build & Deploy to Nexus') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: "${NEXUS_CREDENTIALS_ID}",
                        usernameVariable: 'NEXUS_USER',
                        passwordVariable: 'NEXUS_PASS'
                    )
                ]) {
                    configFileProvider([
                        configFile(
                            fileId: 'maven-settings-nexus',
                            variable: 'MAVEN_SETTINGS'
                        )
                    ]) {
                        sh '''
                            mvn clean deploy -s $MAVEN_SETTINGS
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build & deployment to Nexus successful'
        }
        failure {
            echo 'Build failed'
        }
    }
}
