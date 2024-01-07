pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('89ee9b37-bcac-4f17-bd9a-1d41dda8525b')
        DOCKER_IMAGE_NAME = 'testingovalada/realtime_ping:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE_NAME).run('-p 4000:8080 --name realtime-ping -d')
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push()
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                docker.image(DOCKER_IMAGE_NAME).stop()
                docker.image(DOCKER_IMAGE_NAME).remove()
            }
        }
    }
}
