pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './jenkins/scripts/deliver.sh'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/test-all.sh'
      }
    }

  }
}