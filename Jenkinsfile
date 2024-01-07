def buildImage() {
    stage('Build Image') {
        steps {
            script {
                docker.build("testingovalada/realtime_ping:latest")
            }
        }
    }
}

def runContainer() {
    stage('Run Container') {
        steps {
            script {
                docker.image("testingovalada/realtime_ping:latest").run('-p 4000:8080 --name realtime-ping -d')
            }
        }
    }
}

def pushImage() {
    stage('Push Image to DockerHub') {
        steps {
            script {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                    docker.image("testingovalada/realtime_ping:latest").push()
                }
            }
        }
    }
}

pipeline {
    agent any

    stages {
        buildImage()
        runContainer()
        pushImage()
    }

    post {
        always {
            script {
                docker.image("testingovalada/realtime_ping:latest").stop()
                docker.image("testingovalada/realtime_ping:latest").remove()
            }
        }
    }
}
