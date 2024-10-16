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
      parallel {
        stage('Train') {
          steps {
            sh 'appsec.checkup (train, params = run_id, model_id)'
          }
        }

        stage('Phishing attack') {
          steps {
            sh 'appsec.llm.phishing (params = phi, types = [])'
          }
        }

        stage('Semantick attack') {
          steps {
            sh 'appsec.llm.semantic(params = class_true, new_class, n_world)'
          }
        }

        stage('Backdoor') {
          steps {
            sh 'appsec.llm.backdoor(params = type, trigger = [])'
          }
        }

        stage('Jailbreaking') {
          steps {
            sh 'appsec.llm.laibreaking (params = n_promts)'
          }
        }

        stage('Adv attack') {
          steps {
            sh 'appsec.adv (params = type, hyperparams = [])'
          }
        }

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