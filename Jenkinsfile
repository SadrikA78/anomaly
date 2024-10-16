pipeline {
  agent any
  stages {
    stage('Datasets') {
      parallel {
        stage('Scan Data') {
          steps {
            sh 'appsec.checkup_convert'
          }
        }

        stage('dwwf') {
          steps {
            echo 'ascv'
          }
        }

      }
    }

    stage('Train') {
      steps {
        sh 'appsec.checkup (train, params = run_id, model_id)'
      }
    }

    stage('Product') {
      steps {
        sh 'appsec.checkup (product, params = token)'
      }
    }

  }
}