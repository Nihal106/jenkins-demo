pipeline {
  agent { label 'jenkins-aws' }
  stages {
    stage('Verify Tools') {
      steps {
        sh 'whoami'
        sh 'hostname'
        sh 'which git'
        sh 'git --version'
        sh 'java -version'
        sh 'mvn -version || true'
      }
    }
  }
}
