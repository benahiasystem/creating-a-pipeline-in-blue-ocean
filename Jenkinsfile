pipeline {
  agent {
    docker {
      image 'node:lts-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('build') {
      steps {
        sh 'npm install'
      }
    }

    stage('test') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Select "Proceed" to continue)'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
}