pipeline {
    agent any

    environment {
        dockerImage = "testingovalada/realtime_ping:${env.BUILD_ID}"
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Construye la imagen
                    echo 'Construyendo la imagen Docker...'
                    sh "docker build -t $dockerImage ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Ejecuta el contenedor
                    echo 'Ejecutando el contenedor Docker...'
                    sh "docker run -d --name realtime_ping $dockerImage"
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    // Empuja la imagen a Docker
                    echo 'Empujando la imagen a Docker Hub...'
                    sh "docker push $dockerImage"
                }
            }
        }
    }

    post {
        always {
            // Limpia despues de terminar el pipeline
            echo 'Limpiando...'
            sh "docker stop realtime_ping || true"
            sh "docker rm realtime_ping || true"
            sh "docker rmi $dockerImage"
        }
    }
}
