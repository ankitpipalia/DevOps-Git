pipeline {
  agent any
  stages {
    stage('build') {
      agent any
      steps {
        sh '''cp trainee_backend/.env.example trainee_backend/.env
sed -i \'s/localhost/mongodb/g\' trainee_backend/.env
docker-compose up --build'''
      }
    }

  }
  environment {
    hosturl = 'mongodb://localhost:27017/reactdb'
    PORT = '4000'
  }
}