pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'python:2-alpine'
          //Indicamos usar el tipo de imagen de Python
        }
      }
      steps {
        sh 'python -m py_compile HolaMundo/HolaMundo.py'
        //Se compila la aplicacion
        stash(name: 'resultado-compilado',includes: 'HolaMundo/*.py*')
        //Esto ayuda a guardar el directorio, asi podemos usarlo luego
      }
    }
  }
}
