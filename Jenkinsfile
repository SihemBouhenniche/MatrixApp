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
        mail(subject: 'Build Report', body: 'Le build ‡ bien ÈtÈ effectuÈ.', from: 'fs_bouhenniche@esi.dz', to: 'fm_bourouais@esi.dz')
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
        slackSend(attachments: 'depolyment success', baseUrl: 'https://worksihem.slack.com/services/hooks/jenkins-ci/', message: 'le d√©ploiement √† √©t√© effectu√© avec succ√©es ', token: 'HDIDjUcq505rKhOsFIqxcBGK')
      }
    }
  }
  tools {
    gradle 'GRADLE_LATEST'
  }
}