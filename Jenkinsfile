pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('kbk123')
    }
    stages {
 stage('Get Package Version') {
            steps {
                script {
                    def packageJson = readJSON file: 'api/package.json'
                    def version = packageJson.version
                    // Save the version to an environment variable
                    env.PACKAGE_VERSION = version
                }
            }
        }      
         stage('Build docker image') {
            steps {
                sh "cd api && docker build -t dockerbk1992/lms-be1:${env.PACKAGE_VERSION} ."
                sh"cd webapp && docker build -t dockerbk1992/lms-fe1:${env.PACKAGE_VERSION} ."
            }
        }

          stage('Login to Dockerhub') {
            steps {
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
            }
        }
        stage('Push docker image') {
            steps {
                sh "docker push dockerbk1992/lms-be:${env.PACKAGE_VERSION}"
                sh "docker push dockerbk1992/lms-fe:${env.PACKAGE_VERSION}"
            }
            post {
                always {
                    sh 'docker logout'
                }
            }
        }
    }
}

