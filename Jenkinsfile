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
            sh 'npm run test'
          }
        }
        stage('Send email') {
          steps {
            emailext(subject: 'Aprobar', body: 'Aprobado', attachLog: true, to: 'fer-tester')
          }
        }
      }
    }
    stage('Approve') {
      steps {
        input(message: 'Aprobar?', submitter: 'fer-tester')
      }
    }
    stage('To deploy') {
      steps {
        emailext(subject: 'Deploy', body: 'Deploy', to: 'fer-release')
      }
    }
    stage('To deploy interactive') {
      steps {
        input(message: 'Deploy?', submitter: 'fer-release')
      }
    }
  }
}