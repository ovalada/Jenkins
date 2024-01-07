pipeline {
    agent any

    stages {
        stage('Saludo') {
            steps {
                script {
                    echo '¡Hola desde tu Jenkinsfile!'
                }
            }
        }
    }

    post {
        success {
            script {
                echo '¡Pipeline ejecutado exitosamente!'
            }
        }
        failure {
            script {
                echo '¡El pipeline ha fallado! Por favor, revisa los registros para más detalles.'
            }
        }
    }
}
