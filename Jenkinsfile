pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kbk123')
    }
    stages {
        stage('Build docker image') {
            steps {
                sh "cd api && docker build -t dockerbk1992/lms:$BUILD_NUMBER ."
            }
        }
        stage('Login to Dockerhub') {
            steps {
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
            }
        }
        stage('Push docker image') {
            steps {
                sh "docker push dockerbk1992/lms:$BUILD_NUMBER"
            }
            post {
                always {
                    sh 'docker logout'
                }
            }
        }
    }
}

