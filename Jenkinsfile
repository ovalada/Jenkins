pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "testingovalada/realtime_ping:${env.BUILD_ID}"
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Construye la imagen
                    echo 'Construyendo la imagen Docker...'
                    sh "docker build -t $DOCKER_IMAGE ."
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Ejecuta el contenedor
                    echo 'Ejecutando el contenedor Docker...'
                    sh "docker run -d --name realtime_ping $DOCKER_IMAGE"
                }
            }
        }

stage('Push to Dockerhub') {
    steps {
        script {
            // Empuja la imagen a Docker Hub
            echo 'Empujando la imagen a Docker Hub...'
            withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                sh "docker push $DOCKER_IMAGE"
            }
        }
    }
}
    post {
        always {
            // Limpia después de terminar el pipeline
            echo 'Limpiando...'
            sh "docker stop realtime_ping || true"
            sh "docker rm realtime_ping || true"
            sh "docker rmi $DOCKER_IMAGE"
        }
    }
}
