pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        // uses the SCM configured in the job (recommended)
        checkout scm
      }
    }
    stage('Build') {
      steps {
        echo "Build step - add your build commands here"
      }
    }
    stage('Test') {
      steps {
        echo "Test step - add your tests here"
      }
    }
    stage('Finish') {
      steps {
        echo "Pipeline finished"
      }
    }
  }
}
