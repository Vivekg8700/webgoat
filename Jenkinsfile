pipeline {
    agent any

    tools {
        maven 'M2'
    }

    stages {

        stage('Compile') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')
            }
            steps {
                bat "mvn sonar:sonar -Dsonar.projectKey=Vivekg8700_Centralgit -Dsonar.organization=vivekg8700 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=%SONAR_TOKEN%"
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/**', fingerprint: true
        }
        failure {
            echo 'Build failed. Please check the logs for details.'
        }
    }
}
