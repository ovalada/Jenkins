def docker

pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('89ee9b37-bcac-4f17-bd9a-1d41dda8525b')
        DOCKER_IMAGE_NAME = 'testingovalada/realtime_ping:latest'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    docker = docker.build(DOCKER_IMAGE_NAME)
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Puedes agregar pasos adicionales para construir tu imagen si es necesario
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Puedes agregar pasos adicionales para ejecutar tu contenedor si es necesario
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKERHUB_CREDENTIALS) {
                        docker.image.push()
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Este bloque siempre se ejecutará al finalizar el pipeline
                docker.image.remove() // Elimina la imagen después de empujarla al Docker Hub
            }
        }
    }
}
