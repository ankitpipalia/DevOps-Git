pipeline {
  agent {
    node {
      label 'Jenkins-Slave'
    }

  }
  stages {
    stage('gitclone') {
      steps {
        git 'https://github.com/ankitpipalia/MERN-Stack.git'
      }
    }

    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

    stage('Push') {
      steps {
        sh 'docker tag mern-stack_frontend babodesi/mern-frontend:v$(date +%Y%m%d%H)'
        sh 'docker tag mern-stack_frontend babodesi/mern-backend:v$(date +%Y%m%d%H)'
        sh 'docker push babodesi/mern-frontend:v$(date +%Y%m%d%H)'
        sh 'docker push babodesi/mern-backend:v$(date +%Y%m%d%H)'
      }
    }

  }
  environment {
    DOCKERHUB_CREDENTIALS_PSW = 'ankit@2002'
    DOCKERHUB_CREDENTIALS_USR = 'babodesi'
  }
  post {
    always {
      cleanWs()
      sh 'docker logout'
    }
  }
}