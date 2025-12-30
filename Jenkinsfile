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
                sh 'cmake .'
            }
        }
        stage('Test') {
            steps {
                // just run it
                sh './main'
            }
        }
        stage('Dependency Remove') {
            steps {
                sh "apk del gcc make cmake git"

            }
        }
    }
}