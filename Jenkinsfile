pipeline {
    agent any
    environment { 
        CC = 'g++'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git status'
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
            }
        }
        stage('Build') {
            steps {
                // cmake the project
                sh 'cmake -S . -B build'
                sh 'cmake --build build'
                archiveArtifacts artifacts: 'build/**', fingerprint: true 
            }
        }
        stage('Test') {
            steps {
                // just run it
                sh './build/main'
            }
        }
    }
}