pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './jenkins/build.sh'
      }
    }

    stage('Test') {
      steps {
        echo 'Bees Buzzing!'
        sh './jenkins/test-all.sh'
      }
    }

  }
}