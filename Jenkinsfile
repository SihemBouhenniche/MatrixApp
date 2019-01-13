pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        bat(script: 'gradle build', returnStatus: true, returnStdout: true)
        bat(script: 'gradle javadoc', returnStatus: true, returnStdout: true)
        bat(script: 'gradle uploadArchives', returnStatus: true, returnStdout: true)
      }
    }
    stage('Mail Notification') {
      steps {
        bat(script: 'gradle build', returnStatus: true, returnStdout: true)
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            bat(script: 'sonar-scanner', returnStatus: true, returnStdout: true)
          }
        }
        stage('Test reporting') {
          steps {
            bat(script: 'gradle test', returnStatus: true, returnStdout: true)
          }
        }
      }
    }
    stage('Deployment') {
      steps {
        bat(script: 'gradle uploadArchives', returnStatus: true, returnStdout: true)
      }
    }
    stage('Slack Notification') {
      steps {
        slackSend(attachments: 'depolyment success', baseUrl: 'https://worksihem.slack.com/services/hooks/jenkins-ci/', message: 'le déploiement à été effectué avec succées ', token: 'HDIDjUcq505rKhOsFIqxcBGK')
      }
    }
  }
  tools {
    gradle 'GRADLE_LATEST'
  }
}