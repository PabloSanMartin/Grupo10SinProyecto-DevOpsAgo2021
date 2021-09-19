pipeline {
  agent {
    docker { image 'python:2-alpine' }
  }
  stages {
    stage('Mongo') {
      steps {
        script {
          sh 'docker run --rm -d --name mongo mongo:latest'
          sh 'pip install pymongo'
        }
      }
    }
    stage('Insertar') {
      steps {
        sh 'python InsertarLista.py'
      }
    }
    stage('Ver') {
      steps {
        sh 'python MostrarLista.py'
      }
    }
  }
  post {
        always {
            sh 'stop mongo'
        }
   }
}
