pipeline {
  agent any
  stages {
    stage('error') {
      parallel {
        stage('error') {
          steps {
            echo 'ax'
          }
        }

        stage('dwwf') {
          steps {
            echo 'ascv'
          }
        }

      }
    }

  }
}