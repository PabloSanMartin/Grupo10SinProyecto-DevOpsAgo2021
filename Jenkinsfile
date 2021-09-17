pipeline {
  agent none
  //Usamos none para indicar una imagen especifica en cada stage
  stages {
    stage("build") {
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
     stage("test") {
      agent {
         docker {
          image 'qnib/pytest'
           //Una imagen de testing de python, un container separado
        }
      }
      steps {
        sh 'py.test --verbose --junit-xml test-reporte/resultado.xml HolaMundo/testHolaMundo.py' 
        //Imprime el resultado de testHolaMundo en un xml
      }
       post {
         always {
           junit 'test-reporte/resultado.xml'
           //Muestra el resultado xml
         }
       }
     }
     stage("deploy") {
       agent any
       enviorenment {
         VOLUME = '$(pwd)/HolaMundo:/src'
         IMAGE = 'cdrx/pyinstaller-linux:python2'
         //Crea 2 variables que se usan luego en los pasos del deploy
       }
       steps {
         dir(path: env.BUILD_ID) {
           //Se crea un nuevo sub directorio
           unstash(name: 'resultado-compilado')
           sh "docker run --rm -v ${VOLUME} ${IMAGE} 'pyinstaller -F buildHolaMundo.py'"
           //Comando de pyinstaller que une en una sola aplicacion unica
         }
       }
       post {
         success {
           archiveArtifacts "${env.BUILD_ID}/HolaMundo/dist/buildHolaMundo"
           sh "docker run --rm -v ${VOLUME} ${IMAGE} 'rm -rf build dist'"
           //Archiva la aplicacion unica y muestra lo creado
         }
       }
        
      
    }
  }
}
