pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('SonarQube Code Analysis') {
            steps {
                // Ensure 'SonarQube' matches the Server name configured in Manage Jenkins -> System
                withSonarQubeEnv('SonarQube') {
                    script {
                        // 1. Fetch the exact tool installation path using the explicit type class
                        // 2. Ensure 'sonar-scanner' matches the Name configured in Manage Jenkins -> Tools
                        def scannerHome = tool name: 'sonar-scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        
                        // 3. Execute the scanner using its absolute path
                        sh "${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=Jenkins-Sonarqube-Docker \
                            -Dsonar.projectName=Jenkins-Sonarqube-Docker \
                            -Dsonar.sources=."
                    }
                }
            }
        }
    }
}
