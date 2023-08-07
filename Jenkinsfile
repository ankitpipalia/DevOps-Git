pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_HUB_USERNAME = credentials('docker-hub-username')
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
    sh "docker build -f ./trainee_frontend/Dockerfile -t ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-frontend:v${BUILD_NUMBER}"
    sh "docker tag ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-frontend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-frontend:latest"
    withDockerRegistry(credentialsId: 'docker-hub-credentials') {
        sh "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
        sh "docker push ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-frontend:v${BUILD_NUMBER}"
        sh "docker push ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-frontend:latest"
    }
}

def backendBuildAndPush() {
    sh "docker build -f ./trainee_backend/Dockerfile -t ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-backend:v${BUILD_NUMBER}"
    sh "docker tag ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-backend:v${BUILD_NUMBER} ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-backend:latest"
    withDockerRegistry(credentialsId: 'docker-hub-credentials') {
        sh "docker login -u ${DOCKER_HUB_USERNAME} -p ${DOCKER_HUB_PASSWORD}"
        sh "docker push ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-backend:v${BUILD_NUMBER}"
        sh "docker push ${DOCKER_REGISTRY}/${DOCKER_HUB_USERNAME}/mern-backend:latest"
    }
}