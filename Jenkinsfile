pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_HUB_PASSWORD = credentials('docker-hub-password')
    }

    stages {

        stage('frontend sonarqube') {
            steps {
                sh 'sonar-scanner -Dsonar.projectSettings=/var/lib/jenkins/workspace/MERN-Stack/trainee_frontend/sonar-project.properties'
            }
        }

        stage('backend sonarqube') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/MERN-Stack/trainee_backend/'
                sh 'sonar-scanner -X -Dsonar.login=squ_a8ec9779a12087125885263f7b93b15cdcabac7a'
            }
        }

        stage('Build Backend Docker Images') {
            parallel {
                stage('Build Backend') {
                    steps {
                        script {
                            backendBuildAndPush()
                        }
                    }
                }
            }
        }

        stage('Build Frontend Docker Images') {
            parallel {
                stage('Build Frontend') {
                    steps {
                        script {
                            frontendBuildAndPush()
                        }
                    }
                }
            }
        }

        stage('Cleaning Docker Images') {
            steps {
                script {
                    sh 'docker system prune -a --force'
                }
            }
        }
    }
}

def frontendBuildAndPush() {
    sh "docker build -f /var/lib/jenkins/workspace/MERN-Stack/trainee_frontend/Dockerfile -t ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER} /var/lib/jenkins/workspace/MERN-Stack/trainee_frontend"
    sh "docker tag ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/babodesi/mern-frontend:latest"
    sh "docker login -u babodesi -p ${DOCKER_HUB_PASSWORD}"
    sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER}"
    sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-frontend:latest"

}

def backendBuildAndPush() {
    sh "docker build -f /var/lib/jenkins/workspace/MERN-Stack/trainee_backend/Dockerfile -t ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER} /var/lib/jenkins/workspace/MERN-Stack/trainee_backend"
    sh "docker tag ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/babodesi/mern-backend:latest"
    sh "docker login -u babodesi -p ${DOCKER_HUB_PASSWORD}"
    sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER}"
    sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-backend:latest"
}