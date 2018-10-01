pipeline {
  agent any
  stages {
    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'npm test'
          }
        }
        stage('Send Email') {
          steps {
            emailext(subject: 'Test', body: 'Test Me', to: 'vgoldaracena', from: 'hub@axtel.com.mx')
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