pipeline {
  agent any
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'npm test'
          }
        }
        stage('Send Email') {
          steps {
            emailext(subject: 'Test', body: 'Test Me', to: 'hub', attachLog: true)
          }
        }
      }
    }
    stage('Aprobar') {
      steps {
        input(message: 'Aprobar', submitter: 'hub')
      }
    }
    stage('To Deploy') {
      steps {
        emailext(subject: 'Deploy', attachLog: true, body: 'Hacer deploy', to: 'vgoldaracena')
      }
    }
    stage('Deploy Approve') {
      steps {
        input(message: 'Aprobar', submitter: 'vgoldaracena')
      }
    }
  }
}