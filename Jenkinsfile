pipeline {
  agent any
  options { disableConcurrentBuilds(); skipDefaultCheckout() }

  tools {
    maven 'Maven-3'    // name you set in Global Tool Config
    // optionally jdk 'JDK11' if configured
  }

  stages {
    stage('Checkout') { steps { git branch: 'main', url: 'https://github.com/Nihal106/jenkins-demo.git' } }
    stage('Build')    { steps { echo 'Building...'; bat 'mvn -B clean package' } }
    stage('Test')     { steps { echo 'Running tests...'; bat 'mvn -B test' } }
  }

  post {
    always { echo 'Workspace contents:'; bat 'dir' }
    success { echo 'Build Successful!' }
    failure { echo 'Build Failed!' }
  }
}
