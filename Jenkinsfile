pipeline {
    agent any

    environment {
        // Define the SonarQube server URL and credentials ID (ensure this is configured in Jenkins' global settings)
        SONARQUBE_URL = 'http://13.233.140.129:9000/'
        SONARQUBE_CREDENTIALS_ID = 'sonar-id' // Set this in Jenkins credentials
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Uncomment and run the Maven build command
                // sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'

                // Trigger SonarQube analysis using Maven
                script {
                    withSonarQubeEnv('SonarQube') { 
                        sh 'mvn clean verify sonar:sonar'
                    }
                }

                // If you're using SonarScanner CLI instead of Maven:
                // sh 'sonar-scanner -Dsonar.projectKey=your_project_key -Dsonar.sources=src'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Uncomment and run the Maven test command
                // sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Uncomment and run the deployment command
                // sh 'scp target/myapp.war user@server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            // Actions to take after pipeline execution (like sending notifications)
            echo 'Cleaning up...'
        }
    }
}
