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
       emailext(
        subject: "✅ SUCCESS: ${JOB_NAME} #${BUILD_NUMBER}",
        body: """
Build Status : SUCCESS
Job Name     : ${JOB_NAME}
Build Number : ${BUILD_NUMBER}
Build URL    : ${BUILD_URL}
""",
        to: "nihalpk10006@gmail.com"
      )
    }
    failure {
             emailext(
        subject: "❌ FAILURE: ${JOB_NAME} #${BUILD_NUMBER}",
        body: """
Build Status : FAILED
Job Name     : ${JOB_NAME}
Build Number : ${BUILD_NUMBER}
Check Logs   : ${BUILD_URL}
""",
        to: "nihalpk10006@gmail.com"
      )
    }
  }
}
