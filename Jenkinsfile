pipeline {
    agent any
   stages{
        stage('Build') {
            steps {
                sh'cd api && docker docker build -t dockerbk1992/lms-be .'
                echo 'docker image build..'
                script {
                    docker.build("lms:${env.VERSION}")
                }
            }
        }
        stage('Push to Docker Registry') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/u/dockerbk1992', 'dockerbk1992/Kishore@92') {
                        docker.image("your-image-name:${env.VERSION}").push()
                    }
                }
            }
        }
            }
        }

//kjkjgkhgkjg