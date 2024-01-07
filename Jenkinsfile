pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Construyendo el proyecto...'
                    // Ejemplo: Construir con Maven
                    sh 'mvn clean install'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Ejecutando pruebas...'
                    // Ejemplo: Ejecutar pruebas con Maven
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Desplegando la aplicación...'
                    // Aquí puedes agregar tus propios comandos de implementación
                    // Ejemplo: Desplegar en un servidor de aplicaciones
                    sh 'deploy-script.sh'
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'El pipeline se ejecutó con éxito. ¡Enhorabuena!'
            }
        }
        failure {
            script {
                echo 'El pipeline falló. Por favor, revisa los registros y corrige los problemas.'
            }
        }
    }
}
