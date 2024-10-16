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

        stage('Search phifhing') {
          steps {
            sh 'appsec.phishing ()'
          }
        }

        stage('Search drift') {
          steps {
            sh 'appsec.drift(params = n_groups, b, g)'
          }
        }

        stage('AntiAdv') {
          steps {
            sh 'appsec.antiAdv(param = delta_inference)'
          }
        }

        stage('Set "Water marks"') {
          steps {
            sh 'appsec.water_marking (param = type_data)'
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

    stage('Report') {
      steps {
        sh 'appsec.report (params = json, pdf, docx)'
      }
    }

    stage('Plan') {
      steps {
        sh 'appsec.sheduler (params = days, week)'
        sh 'appsec.check (params = date, id)'
      }
    }

  }
}