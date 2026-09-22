pipeline {
    agent any

    environment {
        IMAGE_NAME = "jenkins-demo"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker images ${IMAGE_NAME}:${IMAGE_TAG}'
                echo 'Basic automated test completed successfully'
            }
        }

        stage('Package') {
            steps {
                sh 'docker save ${IMAGE_NAME}:${IMAGE_TAG} -o ${IMAGE_NAME}.tar'
            }
        }
    }
}
