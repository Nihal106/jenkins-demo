pipeline {
  agent { label 'jenkins-aws' }

  stages {
    stage('Checkout') {
      steps {
        sh '''
          rm -rf jenkins-demo || true
          git clone https://github.com/Nihal106/jenkins-demo.git
          cd jenkins-demo
        '''
      }
    }

    stage('Build') {
      steps {
        sh '''
          cd jenkins-demo
          mvn -B clean package
        '''
      }
    }

    stage('Test') {
      steps {
        sh '''
          cd jenkins-demo
          mvn -B test
        '''
      }
    }
  }
}
