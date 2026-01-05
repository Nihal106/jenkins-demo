pipeline {
  agent { label 'jenkins-aws' }

  options {
    skipDefaultCheckout(true)   // checkout handled manually
    timestamps()
    disableConcurrentBuilds()
  }

  stages {

    stage('Checkout') {
      steps {
        sh '''
          echo "📥 Cloning source code on agent..."
          rm -rf app || true
          git clone https://github.com/Nihal106/jenkins-demo.git app
        '''
      }
    }

    stage('Build') {
      steps {
        sh '''
          echo "🔨 Building application (skip tests)"
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
              echo "🧪 Running unit tests"
              cd app
              mvn -B test
            '''
          }
        }

        stage('Static Checks') {
          steps {
            sh '''
              echo "🔍 Running static validation checks"
              cd app
              mvn -B validate
            '''
          }
        }
      }
    }

    
    // 🔐 ENABLE THIS WHEN SONARQUBE IS READY
    stage('SonarQube Scan') {
      steps {
        withSonarQubeEnv('sonarqube') {
          sh '''
            echo "🔍 Running SonarQube scan"
            cd app
            mvn sonar:sonar
          '''
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 1, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
    

    
    // 🐳 ENABLE WHEN DOCKER IS REQUIRED
    stage('Docker Build') {
      steps {
        sh '''
          echo "🐳 Building Docker image"
          cd app
          docker build -t myapp:1.0 .
        '''
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
