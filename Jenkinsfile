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

        // ✅ ONLY ADD THIS STAGE
        stage('Sonar Analysis') {
            steps {
                bat """
                mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar ^
                  -Dsonar.projectKey=Vivekg8700_Centralgit ^
                  -Dsonar.organization=vivekg8700 ^
                  -Dsonar.host.url=https://sonarcloud.io ^
                  -Dsonar.login=%SONAR_TOKEN%
                """
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
