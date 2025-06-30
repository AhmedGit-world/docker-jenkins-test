pipeline {
    agent any

    environment {
        IMAGE_NAME = "ahmedgitworld/docker-jenkins-test:latest"
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
                    def image = docker.build("${IMAGE_NAME}")
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
                        def image = docker.image("${IMAGE_NAME}")
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
