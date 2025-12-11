// Jenkinsfile - Java + Maven CI/CD (no GitHub required)
pipeline {
  agent any

  tools {
    // Make sure these tool names match your Jenkins global tools configuration
    jdk 'jdk'
  }

  environment {
    MAVEN_OPTS = "-Xmx1024m"
  }

  stages {
    stage('Prepare') {
      steps {
        echo "Workspace path: ${env.WORKSPACE}"
        sh 'mvn -version'
      }
    }

    stage('Clean') {
      steps {
        echo 'Cleaning project...'
        sh 'mvn -B clean'
      }
    }

    stage('Compile') {
      steps {
        echo 'Compiling source code...'
        sh 'mvn -B -DskipTests=true compile'
      }
    }

    stage('Unit Test') {
      steps {
        echo 'Running unit tests...'
        sh 'mvn -B test'
      }
      post {
        always {
          junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
        }
      }
    }

    stage('Package') {
      steps {
        echo 'Packaging project...'
        sh 'mvn -B -DskipTests=true package'
      }
    }

    stage('Static Analysis (optional)') {
      when {
        expression { return fileExists('pom.xml') }
      }
      steps {
        echo '(Optional) Run static code checks or SonarQube here'
        // Example:
        // sh 'mvn -B verify sonar:sonar -Dsonar.login=$SONAR_TOKEN'
      }
    }

    stage('Archive Artifacts') {
      steps {
        echo 'Archiving build artifacts...'
        archiveArtifacts artifacts: 'target/*.jar, target/*.war', allowEmptyArchive: true
      }
    }
  }

  post {
    success {
      echo "Build succeeded: ${env.BUILD_URL}"
    }
    failure {
      echo "Build failed: ${env.BUILD_URL}"
    }
    always {
      echo "Pipeline completed: ${currentBuild.fullDisplayName}"
    }
  }
}

