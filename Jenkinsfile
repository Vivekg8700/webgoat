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
