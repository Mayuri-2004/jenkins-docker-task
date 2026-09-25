pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'docker build -t myapp:${BUILD_NUMBER} .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                sh 'docker images myapp:${BUILD_NUMBER}'
            }
        }

        stage('Docker Image') {
            steps {
                echo 'Docker image created successfully'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop myapp || true
                    docker rm myapp || true

                    docker run -d \
                    --name myapp \
                    -p 8080:80 \
                    myapp:${BUILD_NUMBER}
                '''
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
                sh 'curl -I http://localhost:8080'
            }
        }
    }
}
