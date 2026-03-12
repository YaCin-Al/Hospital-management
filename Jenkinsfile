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

    post {
        success { echo 'Analyse SonarQube terminée !' }
        failure { echo 'Le build ou l\'analyse a échoué.' }
    }
}