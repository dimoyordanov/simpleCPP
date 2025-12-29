pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Setup') {
            steps {
                // install cmake
                sh 'brew install cmake'
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
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}