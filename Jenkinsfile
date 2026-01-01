pipeline {
  agent { label 'jenkins-aws' }

  options {
    skipDefaultCheckout(true)   // 🔥 THIS IS THE FIX
  }

  stages {

    stage('Checkout') {
      steps {
        sh '''
          echo "Cloning source code on agent..."
          rm -rf app || true
          git clone https://github.com/Nihal106/jenkins-demo.git app
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
