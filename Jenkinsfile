pipeline {
    agent any
    
    tools {
        // This tells Jenkins to pull the scanner tool we configured in Step 2
        sonarRunner 'sonar-scanner'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your GitHub main branch
                checkout scm
            }
        }
        
        stage('SonarQube Code Analysis') {
            steps {
                // Change 'SonarQube' to match the system name configured in your Jenkins system settings if needed
                withSonarQubeEnv('SonarQube') {
                    // This executes the actual code scan
                    sh "${tool 'sonar-scanner'}/bin/sonar-scanner \
                    -Dsonar.projectKey=Jenkins-Sonarqube-Docker \
                    -Dsonar.projectName=Jenkins-Sonarqube-Docker \
                    -Dsonar.sources=."
                }
            }
        }
        
        stage("Quality Gate Check") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Optional: This pauses Jenkins until SonarQube finishes processing the queue and returns a Pass/Fail
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
