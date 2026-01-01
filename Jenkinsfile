pipeline {
  agent { label 'jenkins-aws' }

  stages {
    stage('Checkout') {
      steps {
        sh 'which git'
        sh 'git --version'
        git branch: 'main',
            url: 'https://github.com/Nihal106/jenkins-demo.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn -B clean package'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn -B test'
      }
    }
  }
}
