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
    parameters {
        string(name: 'Branch', defaultValue: 'main', description: 'Which branch should i build from?')
        string(name: 'Repository', defaultValue: 'https://github.com/dimoyordanov/simpleCPP.git', description: 'Which repository should i build from?')
    }
    stages {
        stage('Checkout') {
            steps {
                script{
                    if (params.Repository == '' || params.Repository == null) {
                        error "Repository parameter is required."
                    }
                    if (params.Branch == '' || params.Branch == null) {
                        error "Branch parameter is required."   
                    }
                    if (params.Repository != 'https://github.com/dimoyordanov/simpleCPP.git') {
                        error "Trying to run dangerous code!"
                    }
                }
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
                sh 'mkdir build'
                sh 'cppcheck --cppcheck-build-dir=build *.cpp'
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