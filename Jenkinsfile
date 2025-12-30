pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git status'
            }
        }
        stage('Build') {
            steps {
                // cmake the project
                sh 'cmake -S . -B build'
                sh 'cmake --build build'
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