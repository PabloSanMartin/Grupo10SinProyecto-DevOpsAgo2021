pipeline {
  agent {
    docker { image 'python:2-alpine' }
  }
  stages {
    stage('Insert') {
      steps {
        sh 'python -m py_compile HolaMundo/HolaMundo.py'
      }
    }
  }
}
