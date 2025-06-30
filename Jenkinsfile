pipeline {
    agent any

    environment {
        IMAGE_NAME = 'ahmed2472/docker-jenkins-test'
        TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AhmedGit-world/docker-jenkins-test.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        echo 'Logged in to Docker Hub'
                    }
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        def image = docker.image("${IMAGE_NAME}:${TAG}")
                        image.push()
                    }
                }
            }
        }
    }

    post {
        always {
            sh 'docker logout'
        }
    }
}
