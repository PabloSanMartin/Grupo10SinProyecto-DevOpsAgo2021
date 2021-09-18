pipeline {
  agent {
    docker { image 'python:2-alpine' }
  }
  stages {
    stage('Prepare Mongo') {
      steps {
        script {
           sh 'docker run --rm -d --name mongo mongo:latest'
        }
      }
    }
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
  post {
        always {
            sh 'docker stop mongo'
        }
   }
}
