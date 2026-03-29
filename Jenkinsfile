pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
        IMAGE_NAME = 'isenosman/nginx-demo'
    }
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
                echo 'Repository cloned successfully'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
                echo 'Docker image built successfully'
            }
        }
        stage('Push image') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push ${IMAGE_NAME}:${BUILD_NUMBER}'
                echo 'Docker image pushed successfully'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}
