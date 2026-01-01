pipeline {
  agent { label 'jenkins-aws' }

  stages {

    stage('Checkout') {
      steps {
        sh '''
          echo "Cleaning old workspace..."
          rm -rf app || true

          echo "Cloning source code on agent..."
          git clone https://github.com/Nihal106/jenkins-demo.git app

          cd app
          git branch
        '''
      }
    }

    stage('Build') {
      steps {
        sh '''
          cd app
          mvn -B clean package
        '''
      }
    }

    stage('Test') {
      steps {
        sh '''
          cd app
          mvn -B test
        '''
      }
    }
  }

  post {
    success {
      echo '✅ Build Successful'
    }
    failure {
      echo '❌ Build Failed'
    }
  }
}
