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
  environment {
    hosturl = 'mongodb://localhost:27017/reactdb'
    PORT = '4000'
  }
}