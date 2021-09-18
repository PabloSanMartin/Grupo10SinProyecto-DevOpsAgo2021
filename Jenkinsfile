pipeline {
  agent {
    docker { image 'python:2-alpine' }
  }
  stages {
    stage('Prepare Mongo') {
      steps {
        script {
          sh 'run -d -p 27017:27017 --name m1 mongo'
          sh 'pip install pymongo'
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
