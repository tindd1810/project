pipeline {
    agent {
        label 'ubuntu-aws'
    }
    environment {
        REGISTRY_NAME               = credentials('REGISTRY_NAME')
        DOCKER_REGISTRY_USERNAME    = credentials('DOCKER_REGISTRY_USERNAME')
        DOCKER_REGISTRY_PASSWORD    = credentials('DOCKER_REGISTRY_PASSWORD')
    }

    stages {
        stage('git-checkout') {
            steps {
                dir('test-jenkins') {
                    git url: 'https://github.com/tindd1810/project.git'
                }
            }
        }
        stage('docker-build/push-registry') {
            steps {
                sh '''#!/usr/bin/env bash
                cd test-jenkins
                docker login -u ${DOCKER_REGISTRY_USERNAME} -p ${DOCKER_REGISTRY_PASSWORD}
                docker build --tag "${REGISTRY_NAME}/tindd:${BUILD_NUMBER}" .
                docker push "${REGISTRY_NAME}/nodejs-tindd:${BUILD_NUMBER}"
                '''
            }
        }
    }
}