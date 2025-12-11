// Jenkinsfile - Simple (uses mvn available on the agent)
pipeline {
  agent any

  options {
    // avoid concurrent runs for the same branch
    disableConcurrentBuilds()
    // keep logs small (optional)
    buildDiscarder(logRotator(daysToKeepStr: '7', numToKeepStr: '20'))
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        echo 'Running mvn clean package'
        sh 'mvn -B clean package'
      }
      // fail the build fast if mvn command fails
    }

    stage('Test') {
      steps {
        echo 'Running mvn test'
        sh 'mvn -B test'
      }
      post {
        // publish junit reports if tests produce them
        always {
          junit '**/target/surefire-reports/*.xml'
        }
      }
    }

    stage('Archive') {
      steps {
        echo 'Archiving artifacts'
        // Archive any jar/war produced by Maven
        archiveArtifacts artifacts: 'target/*.jar, target/*.war', fingerprint: true, allowEmptyArchive: true
      }
    }
  }

  post {
    success {
      echo "Build Successful!"
    }
    failure {
      echo "Build Failed!"
    }
    always {
      // show workspace contents for debugging
      sh 'echo "Workspace:" && ls -la || true'
    }
  }
}
