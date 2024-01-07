pipeline {
    agent any

    environment {
        // Define variables de entorno si es necesario
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Construir la imagen Docker
                    def dockerImage = docker.build("testingovalada/realtime_ping:latest")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Ejecutar el contenedor Docker
                    def container = dockerImage.run('-p 4000:8080 --name realtime-ping -d')
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    // Subir la imagen a Dockerhub
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        always {
            // Detener y eliminar el contenedor después de la ejecución
            script {
                container.stop()
                container.remove()
            }
        }
    }
}
