pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17'
        }
    }
    // agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Branch Info') {
            steps{
                echo "Building branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Unit Tests') {
            steps {
                bat 'mvn test'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'

            archiveArtifacts '**/target/surefire-reports/*'

            echo "Finished build for branch: ${env.BRANCH_NAME}"
        }

        success {
            echo "SUCCESS: ${env.BRANCH_NAME}"
        }

        failure {
            echo "FAILED: ${env.BRANCH_NAME}"
        }
    }
}