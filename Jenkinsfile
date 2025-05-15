pipeline {
    agent any

    tools {
        maven 'Maven 3.9'  // Match your Maven config name in Jenkins
    }

    environment {
        SONARQUBE = 'MySonarQube'  // Name of SonarQube server in Jenkins config
    }

    stages {
        stage('Checkout') {
            steps {
                // Get code from GitHub
                checkout scm
            }
        }

        stage('Build & Test') {
            steps {
                // Compile and run tests
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube scan using Jenkins SonarQube plugin environment variables
                withSonarQubeEnv(SONARQUBE) {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            // Publish JUnit test results in Jenkins
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
