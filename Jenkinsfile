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
                    checkout scm
                }
            }
        }

        stage('Build Image') {
            steps {
                script {
                    // Puedes agregar pasos adicionales para construir tu imagen si es necesario
                    echo 'Building Docker image...'
                    sh 'docker build -t $DOCKER_IMAGE_NAME .'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Puedes agregar pasos adicionales para ejecutar tu contenedor si es necesario
                    echo 'Running Docker container...'
                    sh 'docker run -d $DOCKER_IMAGE_NAME'
                }
            }
        }

        stage('Push to Dockerhub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: '89ee9b37-bcac-4f17-bd9a-1d41dda8525b', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        echo 'Pushing Docker image to Docker Hub...'
                        sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                        sh 'docker push $DOCKER_IMAGE_NAME'
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                // Este bloque siempre se ejecutará al finalizar el pipeline
                echo 'Cleaning up...'
                sh 'docker rmi $DOCKER_IMAGE_NAME'
            }
        }
    }
}
