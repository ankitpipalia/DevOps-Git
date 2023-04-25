pipeline {
  agent any
  stages {
    stage('build') {
      agent any
      steps {
        sh 'docker-compose up --build'
      }
    }

  }
}