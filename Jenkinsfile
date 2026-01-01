pipeline {
  agent { label 'jenkins-aws' }

  options {
    skipDefaultCheckout(true)   // checkout handled manually
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
          mvn -B clean package -DskipTests
        '''
      }
    }

    stage('Parallel Checks') {
      parallel {

        stage('Unit Tests') {
          steps {
            sh '''
              cd app
              mvn -B test
            '''
          }
        }

        stage('Static Checks') {
          steps {
            sh '''
              cd app
              echo "Running static checks..."
              mvn -B validate
            '''
          }
        }
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
