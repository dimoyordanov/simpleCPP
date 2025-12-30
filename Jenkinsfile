pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
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
        stage('Dependency Remove') {
            steps {
                sh "apk del gcc make cmake git"

            }
        }
    }
}