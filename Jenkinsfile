pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        bat 'gradle uploadArchives'
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Build Report', from: 'fs_bouhenniche@esi.dz', to: 'fm_bourouais@esi.dz', body: 'Le build de projet a bien été effectué')
      }
    }
  }
}