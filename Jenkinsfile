pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        bat(script: 'gradle build', returnStatus: true, returnStdout: true)
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Report', from: 'fs_bouhenniche@esi.dz', to: 'fm_bourouais@esi.dz', body: 'Le build de projet a bien été effectué')
      }
    }
  }
}