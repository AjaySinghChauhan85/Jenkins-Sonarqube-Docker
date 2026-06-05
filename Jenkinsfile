pipeline {
    agent any
    
    tools {
        // The correct block key is 'sonar-scanner'
        'sonar-scanner' 'sonar-scanner' 
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('SonarQube Code Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Use the built-in tool step variable instead of path interpolation
                    def scannerHome = tool 'sonar-scanner'
                    sh "${scannerHome}/bin/sonar-scanner \
                    -Dsonar.projectKey=Jenkins-Sonarqube-Docker \
                    -Dsonar.projectName=Jenkins-Sonarqube-Docker \
                    -Dsonar.sources=."
                }
            }
        }
    }
}
