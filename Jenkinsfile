pipeline {
    agent any

    tools {
        maven 'Maven_3' // Your working Maven tool
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/YaCin-Al/Hospital-management'
            }
        }

        stage('Build & Test') {
            steps {
                bat 'mvn clean verify'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=squ_c17e5a2dcb0e4ce0fc034982c459bcf1f77b907c'
            }
        }
        /*
        // NEW STAGE FOR SONARQUBE
        stage('SonarQube Analysis') {
            steps {
                // This 'withSonarQubeEnv' must match the Server Name from Step 1
                withSonarQubeEnv('SonarLocal') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
    }
    */

    post {
        success { echo 'Analyse SonarQube terminée !' }
        failure { echo 'Le build ou l\'analyse a échoué.' }
    }
}