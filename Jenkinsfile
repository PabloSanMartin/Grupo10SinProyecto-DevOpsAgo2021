pipeline {
  agent { dockerfile true }
  //Usamos none para indicar una imagen especifica en cada stage
  stages {
    stage("build") {
      steps {
        sh 'python -m py_compile HolaMundo/HolaMundo.py'
        //Se compila la aplicacion
      }
    }
  }
}
