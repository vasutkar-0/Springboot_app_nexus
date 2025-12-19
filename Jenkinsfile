pipeline {
    agent any

    environment {
        NEXUS_CREDENTIALS_ID = 'nexus-jenkins-creds'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/vasutkar-0/Springboot_app.git'
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
}
