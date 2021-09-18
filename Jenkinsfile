pipeline {
  agent {
    docker { image 'python:2-alpine' }
  }
  stages {
    stage('Insert') {
      steps {
        sh 'python InsertarLista.py'
      }
    }
    stage('View') {
      steps {
        sh 'python MostrarLista.py'
      }
    }
  }
}
