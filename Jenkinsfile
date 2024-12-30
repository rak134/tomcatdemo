pipeline {
    agent any

    environment {
        // Define the SonarQube server URL
        SONARQUBE_URL = 'http://13.233.140.129:9000/'
        // Define the SonarQube credentials ID and retrieve the token
        SONARQUBE_CREDENTIALS_ID = 'sonar-id'  // Make sure this is set in Jenkins' global credentials
        SONARQUBE_TOKEN = credentials('sqp_77ddb0cdc37745d02db0372f33a63049de8d56c4')  // Use the SonarQube token stored as "Secret text"
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

                // Trigger SonarQube analysis using Maven with additional parameters
                script {
                    // Using SonarQube environment for analysis
                    withSonarQubeEnv('SonarQube') { 
                        // Run the SonarQube analysis with the correct parameters
                        sh """
                            mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=demoapp-project \
                            -Dsonar.host.url=${SONARQUBE_URL} \
                            -Dsonar.login=${SONARQUBE_TOKEN}
                        """
                    }
                }
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
