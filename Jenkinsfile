pipeline {
    agent any

    environment {
        dockerImage = "testingovalada/realtime_ping:${env.BUILD_ID}"
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Construir la imagen Docker
                    echo 'Construyendo la imagen Docker...'
                    sh "sudo docker build -t $dockerImage ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Ejecutar el contenedor Docker
                    echo 'Ejecutando el contenedor Docker...'
                    sh "sudo docker run -d --name realtime_ping $dockerImage"
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    // Empujar la imagen a Docker Hub
                    echo 'Empujando la imagen a Docker Hub...'
                    sh "sudo docker push $dockerImage"
                }
            }
        }
    }

    post {
        always {
            // Limpiar después de completar el pipeline
            echo 'Limpiando...'
            sh "sudo docker stop realtime_ping || true"
            sh "sudo docker rm realtime_ping || true"
            sh "sudo docker rmi $dockerImage"
        }
    }
}
