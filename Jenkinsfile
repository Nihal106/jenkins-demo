pipeline {
  options {
    disableConcurrentBuilds()
    skipDefaultCheckout()
  }

  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Nihal106/jenkins-demo.git'
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        bat 'mvn -B clean package'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        bat 'mvn -B test'
      }
    }
  }

  post {
    success {
      echo 'Build Successful!'
    }
    failure {
      echo 'Build Failed!'
    }
    always {
      echo 'Workspace contents:'
      bat 'dir'
    }
  }
}
