pipeline {
    agent any
    options {
        timestamps()
    }

    post {
        always {
            cleanWs()
        }
    }
    environment { 
        CC = 'g++'
    }
    parameters {
        string(name: 'Branch', defaultValue: 'main', description: 'Which branch should i build from?')
        string(name: 'Repository', defaultValue: 'https://github.com/dimoyordanov/simpleCPP.git', description: 'Which repository should i build from?')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: "*/${params.Branch}"]],
                    userRemoteConfigs: [[url: "${params.Repository}"]]
                ])

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