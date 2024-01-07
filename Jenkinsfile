pipeline {
    agent any
    stages {
        stage('Build Image') {
            steps {
                script {
                    buildImage()
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    runContainer()
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    pushImage()
                }
            }
        }
    }
    post {
        always {
            script {
                // Realiza acciones de limpieza después de la ejecución
            }
        }
    }
}
