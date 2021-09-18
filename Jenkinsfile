pipeline {
    agent {
        docker {
            image 'python:3.9'
            args '--user 0:0'
        }
    }
    stages {
        stage('build') {
            steps {
                sh 'pip install -r requirements.txt'
                sh 'pip install -e .'
            }
        }
        stage('test') {
            steps {
                sh 'coverage run HolaMundo/HolaMundo.py'
            }
            post {
                always {
                    sh 'coverage report'
                }
            }
        }
    }
}
