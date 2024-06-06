pipeline {
    agent any

    stages {
        stage('Build and Push Docker Images') {
            steps {
                script {
                    // Build frontend Docker image
                    docker.build('frontend-image', '-f webapp/Dockerfile ./frontend')
                    // Build backend Docker image
                    docker.build('backend-image', '-f api/Dockerfile ./backend')

                    // Push frontend Docker image to registry
                    docker.withRegistry('https://index.docker.io/v1/', 'kbk123') {
                        docker.image('frontend-image').push('latest')
                    }

                    // Push backend Docker image to registry
                    docker.withRegistry('https://index.docker.io/v1/', 'kbk123') {
                        docker.image('backend-image').push('latest')
                    }
                }
            }
        }
    }
}
