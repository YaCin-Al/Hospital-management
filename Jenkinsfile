pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('1 - Clone') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('2 - Compile') {
            steps {
                echo 'Compiling project...'
                bat 'mvn clean compile'
            }
        }

        stage('3 - Unit Tests') {
            steps {
                echo 'Running unit tests...'
                bat 'mvn test'
            }
        }

        stage('4 - Package') {
            steps {
                echo 'Packaging application...'
                bat 'mvn package -DskipTests'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war, **/target/*.jar', fingerprint: true
                }
            }
        }

        stage('5 - SonarQube Analysis') {
            steps {
                echo 'SonarQube will be configured in next step...'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}