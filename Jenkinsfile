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
        sh 'docker push babodesi/nodeapp_test:latest'
      }
    }

  }
  post {
    always {
      sh 'docker logout'
    }

  }
}