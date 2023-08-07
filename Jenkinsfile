pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_HUB_PASSWORD = credentials('docker-hub-password')
    }

    stages {
    
        stage('Build Frontend Docker Images') {
            parallel {
                stage('Build Frontend') {
                    steps {
                        script {
                            sh 'pwd'
                            sh 'ls'
                            frontendBuildAndPush()
                        }
                    }
                }
            }
        }

        stage('Build Backend Docker Images') {
            parallel {
                stage('Build Backend') {
                    steps {
                        script {
                            sh 'pwd'
                            sh 'ls'
                            backendBuildAndPush()
                        }
                    }
                }
            }
        }
    }
}

def frontendBuildAndPush() {
    sh "docker build -f /var/lib/jenkins/workspace/MERN-Stack/trainee_frontend/Dockerfile -t ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER} /var/lib/jenkins/workspace/MERN-Stack/trainee_frontend"
    sh "docker tag ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/babodesi/mern-frontend:latest"
    withDockerRegistry(credentialsId: 'docker-hub-credentials') {
        sh "docker login -u babodesi -p ${DOCKER_HUB_PASSWORD}"
        sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-frontend:v${BUILD_NUMBER}"
        sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-frontend:latest"
    }
}

def backendBuildAndPush() {
    sh "docker build -f /var/lib/jenkins/workspace/MERN-Stack/trainee_backend/Dockerfile -t ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER} /var/lib/jenkins/workspace/MERN-Stack/trainee_backend"
    sh "docker tag ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/babodesi/mern-backend:latest"
    withDockerRegistry(credentialsId: 'docker-hub-credentials') {
        sh "docker login -u babodesi -p ${DOCKER_HUB_PASSWORD}"
        sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-backend:v${BUILD_NUMBER}"
        sh "docker push ${DOCKER_REGISTRY}/babodesi/mern-backend:latest"
    }
}