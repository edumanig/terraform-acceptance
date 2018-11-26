pipeline {
  agent any
  stages {
    stage('Upgrade Controller') {
      parallel {
        stage('Upgrade Controller') {
          steps {
            addHtmlBadge 'Prepare controller to 4.0'
          }
        }
        stage('upgrade_only') {
          steps {
            build(job: 'upgrade_only', propagate: true, quietPeriod: 10, wait: true)
          }
        }
      }
    }
    stage('Terraform') {
      parallel {
        stage('Terraform') {
          steps {
            addHtmlBadge 'Running Terraform Acceptance'
          }
        }
        stage('tr-acceptance-github') {
          steps {
            build(job: 'tr-acceptance-github', propagate: true, quietPeriod: 10, wait: true)
          }
        }
      }
    }
    stage('Report') {
      steps {
        addHtmlBadge 'Terraform Acceptance Passed - 100%'
        emailext(subject: 'Terraform Acceptance 4.0 Passed 100%', body: 'Terraform Acceptance 4.0 Passed 100%', to: 'edsel@aviatrix.com, arvind@aviatrix.com')
      }
    }
  }
}