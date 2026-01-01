pipeline {
  agent { label 'jenkins-aws' }

  stages {
    stage('Checkout') {
      steps {
        sh '''
          rm -rf app || true
          git clone https://github.com/Nihal106/jenkins-demo.git app
        '''
      }
    }

    stage('Build') {
      steps {
        sh 'cd app && mvn clean package'
      }
    }

    stage('Test') {
      steps {
        sh 'cd app && mvn test'
      }
    }
  }
}
