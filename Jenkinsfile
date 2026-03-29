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
                sh '''
                    export PATH=/usr/local/bin:/opt/homebrew/bin:$PATH
                    docker build -t isenosman/nginx-demo:${BUILD_NUMBER} .
                    echo "Docker image built successfully"
                '''
            }
        }
        stage('Push image') {
            steps {
                sh '''
                    export PATH=/usr/local/bin:/opt/homebrew/bin:$PATH
                    echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                    docker push isenosman/nginx-demo:${BUILD_NUMBER}
                    echo "Docker image pushed successfully"
                '''
            }
        }
    }
    post {
        always {
            sh '''
                export PATH=/usr/local/bin:/opt/homebrew/bin:$PATH
                docker logout
            '''
        }
    }
}
