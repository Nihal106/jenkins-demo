pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        // use the same SCM Jenkins already configured for this pipeline
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
  }
  post {
    success { echo 'Build Successful!' }
    failure { echo 'Build Failed!' }
  }
}
