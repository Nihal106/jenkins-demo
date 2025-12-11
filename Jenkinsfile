// Jenkinsfile (Declarative) — use checkout scm to avoid branch mismatches
pipeline {
  // Prevent concurrent builds and avoid resume after restart (optional policies)
  options {
    disableConcurrentBuilds()
    skipDefaultCheckout()     // we'll explicitly use checkout scm in the Checkout stage
    // you can add buildDiscarder(logRotator(...)) here if desired
  }

  agent any

  stages {
    stage('Checkout') {
      steps {
        // Use the SCM already configured for the job (Pipeline from SCM)
        checkout scm
        // checkout scm
        // If you prefer explicit git with branch:
        // git branch: 'main', url: 'https://github.com/Nihal106/jenkins-demo.git'
        git branch: 'main', url: 'https://github.com/Nihal106/jenkins-demo.git'
      }
    }

    stage('Build') {
      steps {
        echo 'Building...'
        // Use Maven if your project uses Maven. Adjust if using gradle/npm etc.
        sh 'mvn -B clean package'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests...'
        sh 'mvn -B test'
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
      // useful cleanup/diagnostics: list workspace
      sh 'echo "Workspace contents:"; ls -la || true'
    }
  }
}
