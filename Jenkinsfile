pipeline {
    agent any
      stages {
        stage('Build Image') {
          steps {
            script {
              docker.build("testingovalada/realtime_ping:latest")
            }
          }
        }

        stage('Run Container') {
          steps {
            script {
              docker.image("testingovalada/realtime_ping:latest").run()
            }
          }
        }

        stage('Push to Dockerhub') {
          steps {
            script {
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
                docker.image("testingovalada/realtime_ping:latest").push()
              }
            }
          }
        }
      }
    }
